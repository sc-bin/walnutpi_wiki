---
sidebar_position: 2
---

# YOLO11 Classification

This model classifies images, outputting the probability of what an object is.

![result](./img/classify/example_cls.jpg)

## Prepare Model File

The program package we provide includes a file named `yolo11n-cls.nb`, which is the model file for running YOLO11 classification on the WalnutPi 2B (T527) NPU.

![result](./img/classify/cls1.png)

If you want to try converting the model yourself, refer to: [Model Conversion Tutorial](./model_convert.md)

## Install OpenCV

This tutorial requires the OpenCV library. For installation instructions, refer to: [OpenCV Installation](../../opencv/install.md)

## Run Model with Python

WalnutPi 2B v1.3.0 and above provides a packaged YOLO11 Python library.

### 1. Instantiate yolo11 Class
Instantiate the `YOLO11_CLS` class by passing the model file path:
```python
from walnutpi import YOLO11
yolo = YOLO11.YOLO11_CLS("model/yolo11n-cls.nb")
```
### 2. Run Model - Blocking Mode
Use the `run` method to run the model and get detection results.

Pass the image data, which can be read using OpenCV's image reading method:
```python
# Read image
import cv2
img = cv2.imread("image/banana.jpg")

# Detect
result = yolo.run(img)
```

### 3. Run Model - Non-blocking Mode

::::tip Note
Non-blocking mode is primarily used for camera capture scenarios. When inference is slower than the camera, using the non-blocking method won't affect camera image capture, and the display won't appear to slow down.
::::

Use the `run_async` method, which creates a thread to run the model and returns immediately. It takes 3 parameters:
- Image data, read using OpenCV's image reading method
- Confidence threshold, only detection boxes above this confidence will be returned
- Detection box overlap threshold, the model often hits multiple boxes around an object. If the area overlap between boxes exceeds this value, only the box with the highest confidence is kept, and other overlapping boxes are removed

Non-blocking mode works with the `is_running` property, which has a value of `true` or `false`, indicating whether a `run_async` model thread is running in the background. If a thread is already running, calling `run_async` again won't start a new thread. You can also use this property to check if the model thread has finished and results are ready.

Use the `get_result()` method to return the background recognition result, which is the same as what the blocking `run` method returns:

```python
import cv2
img = cv2.imread("image/banana.jpg")

yolo.run_async(img)
while yolo.is_running:
    time.sleep(0.1)
result = yolo.get_result()
```

### 4. Detection Results
Both the `run` method and `get_result` method return a classification result object with the following two properties:

| Property | Description                            |
| ---- | ------------------------------- |
| top5 | List containing the top 5 categories by confidence |
| all  | List containing confidence values for all categories    |

The `top5` property is a list containing 5 objects, each with the following two properties:

| Property    | Description   |
| ----------- | ------ |
| label       | Category   |
| reliability | Confidence |

Note that `label` is a number. For example, the official YOLO model was trained with 1000 annotated categories, so the `label` property will be 0-999.

The `all` property is a list where each value represents the confidence of the category at that position. For example, `all[15]` is the confidence of category 15.

The following code can be used to output the top 5 category information:
```python
for i in result.top5:
    print(
        "{:f} {:d}".format(
            i.reliability,
            i.label,
        )
    )
"""
# Output:
0.644337 954
0.519933 114
0.515940 110
0.510992 600
0.506065 679
"""
```

You can also check the confidence of a specific category. For example, if banana is 954, use the following code to check only banana's confidence:
```python
print(f"Probability that this image is a banana: {result.all[954]}")
```
## Example Programs

Copy the entire YOLO11 folder from the resource package to the WalnutPi 2B. Run the code using the built-in Thonny or terminal Python.

![result](./img/classify/cls2.png)

The official YOLO classification model was trained with 1000 annotated categories. When the model runs, it only outputs the category index; you need to retrieve the category name yourself.

A file named `dataset_ImageNet.py` is provided, which stores category names in an array for easy use in code:
```python
label_names = ["tench","goldfish","great white shark","tiger shark","hammerhead shark","electric ray","stingray","cock","hen","ostrich","brambling","goldfinch","house finch","junco","indigo bunting","American robin","bulbul","jay","magpie","chickadee","American dipper","kite","bald eagle","vulture","great grey owl","fire salamander","smooth newt","newt","spotted salamander","axolotl","American bullfrog","tree frog","tailed frog","loggerhead sea turtle","leatherback sea turtle","mud turtle","terrapin","box turtle","banded gecko","green iguana","Carolina anole","desert grassland whiptail lizard","agama","frilled-necked lizard","alligator lizard","Gila monster","European green lizard","chameleon","Komodo dragon","Nile crocodile","American alligator","triceratops","worm snake","ring-necked snake","eastern hog-nosed snake","smooth green snake","kingsnake","garter snake","water snake","vine snake","night snake","boa constrictor","African rock python","Indian cobra","green mamba","sea snake","Saharan horned viper","eastern diamondback rattlesnake","sidewinder","trilobite","harvestman","scorpion","yellow garden spider","barn spider","European garden spider","southern black widow","tarantula","wolf spider","tick","centipede","black grouse","ptarmigan","ruffed grouse","prairie grouse","peacock","quail","partridge","grey parrot","macaw","sulphur-crested cockatoo","lorikeet","coucal","bee eater","hornbill","hummingbird","jacamar","toucan","duck","red-breasted merganser","goose","black swan","tusker","echidna","platypus","wallaby","koala","wombat","jellyfish","sea anemone","brain coral","flatworm","nematode","conch","snail","slug","sea slug","chiton","chambered nautilus","Dungeness crab","rock crab","fiddler crab","red king crab","American lobster","spiny lobster","crayfish","hermit crab","isopod","white stork","black stork","spoonbill","flamingo","little blue heron","great egret","bittern","crane (bird)","limpkin","common gallinule","American coot","bustard","ruddy turnstone","dunlin","common redshank","dowitcher","oystercatcher","pelican","king penguin","albatross","grey whale","killer whale","dugong","sea lion","Chihuahua","Japanese Chin","Maltese","Pekingese","Shih Tzu","King Charles Spaniel","Papillon","toy terrier","Rhodesian Ridgeback","Afghan Hound","Basset Hound","Beagle","Bloodhound","Bluetick Coonhound","Black and Tan Coonhound","Treeing Walker Coonhound","English foxhound","Redbone Coonhound","borzoi","Irish Wolfhound","Italian Greyhound","Whippet","Ibizan Hound","Norwegian Elkhound","Otterhound","Saluki","Scottish Deerhound","Weimaraner","Staffordshire Bull Terrier","American Staffordshire Terrier","Bedlington Terrier","Border Terrier","Kerry Blue Terrier","Irish Terrier","Norfolk Terrier","Norwich Terrier","Yorkshire Terrier","Wire Fox Terrier","Lakeland Terrier","Sealyham Terrier","Airedale Terrier","Cairn Terrier","Australian Terrier","Dandie Dinmont Terrier","Boston Terrier","Miniature Schnauzer","Giant Schnauzer","Standard Schnauzer","Scottish Terrier","Tibetan Terrier","Australian Silky Terrier","Soft-coated Wheaten Terrier","West Highland White Terrier","Lhasa Apso","Flat-Coated Retriever","Curly-coated Retriever","Golden Retriever","Labrador Retriever","Chesapeake Bay Retriever","German Shorthaired Pointer","Vizsla","English Setter","Irish Setter","Gordon Setter","Brittany","Clumber Spaniel","English Springer Spaniel","Welsh Springer Spaniel","Cocker Spaniels","Sussex Spaniel","Irish Water Spaniel","Kuvasz","Schipperke","Groenendael","Malinois","Briard","Australian Kelpie","Komondor","Old English Sheepdog","Shetland Sheepdog","collie","Border Collie","Bouvier des Flandres","Rottweiler","German Shepherd Dog","Dobermann","Miniature Pinscher","Greater Swiss Mountain Dog","Bernese Mountain Dog","Appenzeller Sennenhund","Entlebucher Sennenhund","Boxer","Bullmastiff","Tibetan Mastiff","French Bulldog","Great Dane","St. Bernard","husky","Alaskan Malamute","Siberian Husky","Dalmatian","Affenpinscher","Basenji","pug","Leonberger","Newfoundland","Pyrenean Mountain Dog","Samoyed","Pomeranian","Chow Chow","Keeshond","Griffon Bruxellois","Pembroke Welsh Corgi","Cardigan Welsh Corgi","Toy Poodle","Miniature Poodle","Standard Poodle","Mexican hairless dog","grey wolf","Alaskan tundra wolf","red wolf","coyote","dingo","dhole","African wild dog","hyena","red fox","kit fox","Arctic fox","grey fox","tabby cat","tiger cat","Persian cat","Siamese cat","Egyptian Mau","cougar","lynx","leopard","snow leopard","jaguar","lion","tiger","cheetah","brown bear","American black bear","polar bear","sloth bear","mongoose","meerkat","tiger beetle","ladybug","ground beetle","longhorn beetle","leaf beetle","dung beetle","rhinoceros beetle","weevil","fly","bee","ant","grasshopper","cricket","stick insect","cockroach","mantis","cicada","leafhopper","lacewing","dragonfly","damselfly","red admiral","ringlet","monarch butterfly","small white","sulphur butterfly","gossamer-winged butterfly","starfish","sea urchin","sea cucumber","cottontail rabbit","hare","Angora rabbit","hamster","porcupine","fox squirrel","marmot","beaver","guinea pig","common sorrel","zebra","pig","wild boar","warthog","hippopotamus","ox","water buffalo","bison","ram","bighorn sheep","Alpine ibex","hartebeest","impala","gazelle","dromedary","llama","weasel","mink","European polecat","black-footed ferret","otter","skunk","badger","armadillo","three-toed sloth","orangutan","gorilla","chimpanzee","gibbon","siamang","guenon","patas monkey","baboon","macaque","langur","black-and-white colobus","proboscis monkey","marmoset","white-headed capuchin","howler monkey","titi","Geoffroy's spider monkey","common squirrel monkey","ring-tailed lemur","indri","Asian elephant","African bush elephant","red panda","giant panda","snoek","eel","coho salmon","rock beauty","clownfish","sturgeon","garfish","lionfish","pufferfish","abacus","abaya","academic gown","accordion","acoustic guitar","aircraft carrier","airliner","airship","altar","ambulance","amphibious vehicle","analog clock","apiary","apron","waste container","assault rifle","backpack","bakery","balance beam","balloon","ballpoint pen","Band-Aid","banjo","baluster","barbell","barber chair","barbershop","barn","barometer","barrel","wheelbarrow","baseball","basketball","bassinet","bassoon","swimming cap","bath towel","bathtub","station wagon","lighthouse","beaker","military cap","beer bottle","beer glass","bell-cot","bib","tandem bicycle","bikini","ring binder","binoculars","birdhouse","boathouse","bobsleigh","bolo tie","poke bonnet","bookcase","bookstore","bottle cap","bow","bow tie","brass","bra","breakwater","breastplate","broom","bucket","buckle","bulletproof vest","high-speed train","butcher shop","taxicab","cauldron","candle","cannon","canoe","can opener","cardigan","car mirror","carousel","tool kit","carton","car wheel","automated teller machine","cassette","cassette player","castle","catamaran","CD player","cello","mobile phone","chain","chain-link fence","chain mail","chainsaw","chest","chiffonier","chime","china cabinet","Christmas stocking","church","movie theater","cleaver","cliff dwelling","cloak","clogs","cocktail shaker","coffee mug","coffeemaker","coil","combination lock","computer keyboard","confectionery store","container ship","convertible","corkscrew","cornet","cowboy boot","cowboy hat","cradle","crane (machine)","crash helmet","crate","infant bed","Crock Pot","croquet ball","crutch","cuirass","dam","desk","desktop computer","rotary dial telephone","diaper","digital clock","digital watch","dining table","dishcloth","dishwasher","disc brake","dock","dog sled","dome","doormat","drilling rig","drum","drumstick","dumbbell","Dutch oven","electric fan","electric guitar","electric locomotive","entertainment center","envelope","espresso machine","face powder","feather boa","filing cabinet","fireboat","fire engine","fire screen sheet","flagpole","flute","folding chair","football helmet","forklift","fountain","fountain pen","four-poster bed","freight car","French horn","frying pan","fur coat","garbage truck","gas mask","gas pump","goblet","go-kart","golf ball","golf cart","gondola","gong","gown","grand piano","greenhouse","grille","grocery store","guillotine","barrette","hair spray","half-track","hammer","hamper","hair dryer","hand-held computer","handkerchief","hard disk drive","harmonica","harp","harvester","hatchet","holster","home theater","honeycomb","hook","hoop skirt","horizontal bar","horse-drawn vehicle","hourglass","iPod","clothes iron","jack-o'-lantern","jeans","jeep","T-shirt","jigsaw puzzle","pulled rickshaw","joystick","kimono","knee pad","knot","lab coat","ladle","lampshade","laptop computer","lawn mower","lens cap","paper knife","library","lifeboat","lighter","limousine","ocean liner","lipstick","slip-on shoe","lotion","speaker","loupe","sawmill","magnetic compass","mail bag","mailbox","tights","tank suit","manhole cover","maraca","marimba","mask","match","maypole","maze","measuring cup","medicine chest","megalith","microphone","microwave oven","military uniform","milk can","minibus","miniskirt","minivan","missile","mitten","mixing bowl","mobile home","Model T","modem","monastery","monitor","moped","mortar","square academic cap","mosque","mosquito net","scooter","mountain bike","tent","computer mouse","mousetrap","moving van","muzzle","nail","neck brace","necklace","nipple","notebook computer","obelisk","oboe","ocarina","odometer","oil filter","organ","oscilloscope","overskirt","bullock cart","oxygen mask","packet","paddle","paddle wheel","padlock","paintbrush","pajamas","palace","pan flute","paper towel","parachute","parallel bars","park bench","parking meter","passenger car","patio","payphone","pedestal","pencil case","pencil sharpener","perfume","Petri dish","photocopier","plectrum","Pickelhaube","picket fence","pickup truck","pier","piggy bank","pill bottle","pillow","ping-pong ball","pinwheel","pirate ship","pitcher","hand plane","planetarium","plastic bag","plate rack","plow","plunger","Polaroid camera","pole","police van","poncho","billiard table","soda bottle","pot","potter's wheel","power drill","prayer rug","printer","prison","projectile","projector","hockey puck","punching bag","purse","quill","quilt","race car","racket","radiator","radio","radio telescope","rain barrel","recreational vehicle","reel","reflex camera","refrigerator","remote control","restaurant","revolver","rifle","rocking chair","rotisserie","eraser","rugby ball","ruler","running shoe","safe","safety pin","salt shaker","sandal","sarong","saxophone","scabbard","weighing scale","school bus","schooner","scoreboard","CRT screen","screw","screwdriver","seat belt","sewing machine","shield","shoe store","shoji","shopping basket","shopping cart","shovel","shower cap","shower curtain","ski","ski mask","sleeping bag","slide rule","sliding door","slot machine","snorkel","snowmobile","snowplow","soap dispenser","soccer ball","sock","solar thermal collector","sombrero","soup bowl","space bar","space heater","space shuttle","spatula","motorboat","spider web","spindle","sports car","spotlight","stage","steam locomotive","through arch bridge","steel drum","stethoscope","scarf","stone wall","stopwatch","stove","strainer","tram","stretcher","couch","stupa","submarine","suit","sundial","sunglass","sunglasses","sunscreen","suspension bridge","mop","sweatshirt","swimsuit","swing","switch","syringe","table lamp","tank","tape player","teapot","teddy bear","television","tennis ball","thatched roof","front curtain","thimble","threshing machine","throne","tile roof","toaster","tobacco shop","toilet seat","torch","totem pole","tow truck","toy store","tractor","semi-trailer truck","tray","trench coat","tricycle","trimaran","tripod","triumphal arch","trolleybus","trombone","tub","turnstile","typewriter keyboard","umbrella","unicycle","upright piano","vacuum cleaner","vase","vault","velvet","vending machine","vestment","viaduct","violin","volleyball","waffle iron","wall clock","wallet","wardrobe","military aircraft","sink","washing machine","water bottle","water jug","water tower","whiskey jug","whistle","wig","window screen","window shade","Windsor tie","wine bottle","wing","wok","wooden spoon","wool","split-rail fence","shipwreck","yawl","yurt","website","comic book","crossword","traffic sign","traffic light","dust jacket","menu","plate","guacamole","consomme","hot pot","trifle","ice cream","ice pop","baguette","bagel","pretzel","cheeseburger","hot dog","mashed potato","cabbage","broccoli","cauliflower","zucchini","spaghetti squash","acorn squash","butternut squash","cucumber","artichoke","bell pepper","cardoon","mushroom","Granny Smith","strawberry","orange","lemon","fig","pineapple","banana","jackfruit","custard apple","pomegranate","hay","carbonara","chocolate syrup","dough","meatloaf","pizza","pot pie","burrito","red wine","espresso","cup","eggnog","alp","bubble","cliff","coral reef","geyser","lakeshore","promontory","shoal","seashore","valley","volcano","baseball player","bridegroom","scuba diver","rapeseed","daisy","yellow lady's slipper","corn","acorn","rose hip","horse chestnut seed","coral fungus","agaric","gyromitra","stinkhorn mushroom","earth star","hen-of-the-woods","bolete","ear","toilet paper",]

```

### Image-Based

```python
'''
Experiment Name: YOLO11 Classification
Experiment Platform: WalnutPi 2B
Description: Image recognition
'''

from walnutpi import YOLO11
import dataset_ImageNet
import cv2

# [Optional] Allow Thonny remote execution
import os
os.environ["DISPLAY"] = ":0.0"

model_path = "model/yolo11n-cls.nb" # Model path
picture_path = "image/banana.jpg" # Image path
output_path = "result.jpg" # Output result save path

# Read image
img = cv2.imread(picture_path)

# Detect image
yolo = YOLO11.YOLO11_CLS(model_path)
result = yolo.run(img)

# Output results and draw on image
index = 0
for i in result.top5:
    show_string = "{:f} {:s}".format(
        i.reliability,
        dataset_ImageNet.label_names[i.label],
    )
    print(show_string)
    index += 1

    cv2.putText(
        img,
        show_string,
        (10, 30 * index),
        cv2.FONT_HERSHEY_SIMPLEX,
        1,
        (0, 0, 200),
        2,
    )

# Save image
cv2.imwrite(output_path, img)

# Display image in window
cv2.imshow('result',img)

cv2.waitKey() # Wait for any key press
cv2.destroyAllWindows() # Close window
```

![result](./img/classify/example_cls_picture.jpg)

### Camera-Based

You can first learn about the [USB Camera Usage Tutorial](../../opencv/usb_cam.md) in OpenCV.

```python
'''
Experiment Name: YOLO11 Classification
Experiment Platform: WalnutPi 2B
Description: Camera capture recognition
'''

from walnutpi import YOLO11
import dataset_ImageNet
import cv2,time

# [Optional] Allow Thonny remote execution
import os
os.environ["DISPLAY"] = ":0.0"

# Load model
model_path = "model/yolo11n-cls.nb"
yolo = YOLO11.YOLO11_CLS(model_path)

# Open camera
cap = cv2.VideoCapture(0)
if not cap.isOpened():
    print("Cannot open camera")
    exit()

# Set to 1080p
#cap.set(cv2.CAP_PROP_FOURCC, cv2.VideoWriter_fourcc(*"MJPG"))
#cap.set(cv2.CAP_PROP_FRAME_WIDTH, 1920)  # Set width
#cap.set(cv2.CAP_PROP_FRAME_HEIGHT, 1080)  # Set height

# Calculate FPS
count=0
pt=0
fps = 0


while True:
    
    # Calculate FPS
    count+=1    
    if time.time()-pt >=1 : # Over 1 second
        
        fps=1/((time.time()-pt)/count)# Calculate FPS
        print(fps)
        count=0
        pt=time.time()
    
    # Read a frame from camera
    ret, img = cap.read()
    
    if not ret:
        print("Can't receive frame (stream end?). Exiting ...")
        break
    
    # Inference frame
    if not yolo.is_running:
        yolo.run_async(img)
    result = yolo.get_result()

    
    # Process output results
    index = 0
    
    if result is not None:
        
        for i in result.top5:
            
            show_string = "{:.2f} {:s}".format(i.reliability, dataset_ImageNet.label_names[i.label])
            
            index += 1
            
            # Print results
            print(show_string)
            
            # Draw results
            cv2.putText(img, show_string, (10, 50+30 * index), cv2.FONT_HERSHEY_SIMPLEX, 1, (0, 0, 255), 2)        
    
    cv2.putText(img, 'FPS: '+str(fps), (10,30), cv2.FONT_HERSHEY_SIMPLEX, 1, (0,0,255), 2) # Draw FPS on image
    
    cv2.imshow("result", img)# Display image in window
    
    key = cv2.waitKey(1) # Window refresh interval of 1ms to prevent blocking    
    if key == 32: # Press space key to exit
        break
    
cap .release() # Release camera
cv2.destroyAllWindows() # Destroy camera video window
```

![result](./img/classify/example_cls_camera.jpg)
