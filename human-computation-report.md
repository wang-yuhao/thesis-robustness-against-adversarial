---
title: "landmARTigo: A game that allows users to identify and geolocate landmarks depicted in artworks"
author:
    - Gregor Anzer
    - Fabian Braun
    - Florian Edelmann
    - Yuhao Wang
teamname: Gutsy Gibbons
preliminary: true
autoSectionLabels: true
cref: true
---


##### Abstract

This project draft envisions the human computation system *landmARTigo* that leverages the human perception and knowledge of real users to identify landmarks that might be depicted in artworks. The system is similar to the *ESP game*, *ARTigo* and *Karido*. To incentivize users, we elaborated several benefits for users and stakeholders. We also developed a concept for the user interface. The draft includes a model for data processing and the algorithms involved in the human computation system. The system has to deal with the cold-start problem, which we want to mitigate with several solutions. We devised metrics for evaluation and how to execute the evaluation. For future work, there are several extensions we came up with, that are possible, if the system is successful.

## Introduction

<!--
### Related information on the topic field (0.5 - 1 page)

* Yuhao 

* ESP-Game related
* Location-related
-->
In the past few decades, with the rapid development of the world economy, the global tourism industry has become increasingly prosperous. At the same time modelling and recognizing landmarks at world-scale became a very important yet challenging task. Besides we don’t have readily available datasets for global landmarks. Getting reliable visual models for landmarks will also cause some challenges for us, the search efficiency of a large scale system is another problem. In order to solve these difficulties, using an ESP-like game [@von2004labeling] is the most suitable method. Through an online map users can easily explore artwork around their location. Of course that is not the only functionality, other developers can also implement further work by helping this human computation system. It could be possible to further enhance the location data through machine learning. The output from playing the game could be used as input for our filtering method for input data. Among other functions, a function to find a specific artwork that a user knows its location of could be implemented.

### Motivation
The purpose of the system that we devised is to add landmark tags to artworks that depict landmarks.
The scientific interest in art is what mainly motivates us to contribute landmarks to the data related to artworks. Having a large database of artworks that are tagged with a landmark that they depict can have multiple benefits. The data can be used as input for machine learning. Google's landmark recognition engine is one example for machine learning and landmark recognition. The data could also be relevant for historic research, as the database we use also contains historic landmarks. Another worthy goal of our system is to foster our users' interest in art, which is used as a motivation mechanism.
The application is designed to have a map showing the user's location and all the landmarks in their area, together with the artworks depicting them. For interested users, this allows getting notified when they are close to some tagged artwork.

### Related Work
In human computation, human abilities are still needed to perform tasks, which are not yet solely solvable by computers. One such ability is the human visual perception. Recognizing artworks is still not completely possible for computers. But many systems already exist to benefit from human perception for tagging artworks.

The core of our proposed GWAP (Game With A Purpose [@von2008designing]) is designed like the ESP game [@von2004labeling]. The ESP game is a two player random matching game utilizing human computation. In this game each player is randomly paired with another user whose identity they do not know. Both players are shown the same images and are told to enter the label that they think the other player would enter. If they can agree on a word, it is considered to be a valid label for the respective image and added to the database; both players are then awarded in-game points.

The system we propose in this paper is called *landmARTigo* and builds upon the ESP game by allowing users to tag locations of landmarks that are depicted in the shown images of artworks. It is designed to be part of the *ARTigo* ecosystem that aims to collect data about artworks in order to improve search engines for art [@2013artigo]. To ensure a certain quality of the resulting location tags, our system applies a two step validation, with the second step being enabled by a modified DBSCAN clustering algorithm[@ester1996density]
(see [@sec:algorithm-for-data-aggregation]).

<!--
shortened version above: To ensure a certain....
### Data processing
The entered data of the players must be validated in order to prevent the collection of wrong location data into the core data pool. The validation process consists of two steps; instant validation and delayed validation (see [@sec:algorithm-for-data-aggregation]). As soon as a new location tag is added to a picture, the DBSCAN clustering algorithm [@ester1996density] is executed. The resulting clusters have a density value which, if they exceed a certain threshold, determine their validity. Occasionally, the system will show already tagged pictures to users as a task to check whether they maliciously input wrong data. In addition, the time of players to complete tasks will be measured, so that irregularities are filtered by the system.
-->

### Purpose of the HC system

<!--
### Purpose of the HC system (0.5 page)
*Flo*
-->

The main purpose of the proposed human computation system *landmARTigo* is the contribution of valuable location data about depicted landmarks to the *ARTigo* database to enable use cases like data-driven research in art history.

There are, however, three specific use cases targeting a larger audience besides research that could be solved using the collected data.

The first scenario is seeing an artwork with a landmark, e.g. in the museum, and being able to tell which landmark is depicted and where it is located, e.g. because one wants to visit it in real life (*Search by artwork*).

The other two scenarios are essentially the other way around: Consider being a tourist in another town. It could be interesting to find all artworks that depict a landmark you have seen (*Search by landmark*) or some landmarks in the area you want to explore (*Search by location*).

<!-- 
### Human contribution to the system (0.5 page) 
*Yuhao*
-->
## Human contribution to the system
The GWAP we propose is a human computation system, thus we make use of both digital processing and human intelligence to analyze and improve geolocation data. The users do not just play the game to be entertained, but also contribute their considerable knowledge and expertise to the system, which helps both the research community and other applications that make use of that data (see [@sec:purpose-of-the-hc-system]).

### Gather Information
First the most import work of human intelligence is collecting a large information set in the system. As more and more users participate in our system, we can collect a huge amount of geolocation data. These data not only involve different artworks and landmarks, but are also collected from users in different countries and environments, diversifying and improving the data a lot.

To make the task easier and more enjoyable for the players, only artworks from the *ARTigo* database are selected that are likely to depict a landmark based on the labels associated with the artwork. Also, artworks with an existing geolocation tag are preferred in the game (besides random images out of the aforementioned selection) if that location is near the user. Using this selection mechanism, users can more often tag a location rather than just clicking "not a landmark" or "I don't know".

### Analyzing Data
Secondly, people can help us improve fuzzy or incomplete geolocation data. The resulting locations from users playing the game is more accurate than machine recognition because a sufficiently high number of people agrees on them. For machine learning, a large dataset with tagged input data, i.e. artworks with landmarks and their locations, would be needed, which is not available yet. Especially the information analysis of unusual pictures like artworks is still a hard challenge for today's technology. In this field the human intelligence makes up for the deficiency of computers effectively.


## Functionality of a novel HC system
<!-- *Gregor* -->
The functionality of our novel human computation system can be divided into the functionality as seen by the users, and the functionality as seen by the maintainers and researchers behind *landmARTigo*.

### Functionality as seen by a user
<!-- 0.5 page - 1 page -->
The user of our HC system that we are primarily catering to is anyone with an inherent interest in art enjoying a round-based game about artworks. It also encourages discovering artworks in places you have been or near the area your are currently in. These two types can be further split up.

#### The Game
The user has the possibility to play a round of the game. They will be paired up with another player (to verify the data). The user is then presented with a predefined amount of artworks that possibly contain landmarks. They are shown one artwork at a time. Then they have to decide to either pick the location of the depicted landmark, skip this artwork, or mark it as an artwork that does not contain a landmark. If they are able to identify a landmark in the depicted artwork, they will be presented with an interactive map to pinpoint the location of the landmark which they saw. If they cannot locate an art piece, they can skip it without any delay. Users will receive points for correctly tagged locations. If the system cannot yet confirm that a landmark is correct, they will get points later on if they are logged in. After a round the player is presented with a summary and can look at the artwork again. They are also able to see the points they gained and review their decision for each artwork. Additional information displayed are title and artist of the artwork (possibly also the year of creation and further data if needed). Optionally, logged in users can retain their summaries.

#### Exploration
A big part of the long term motivation for our users is the exploration of artworks around the world and especially the ones close to our users.
In the game part, the user can already explore artworks by playing rounds and getting to see (pseudo-)random images of artworks.

Additionally we imagine our system installed on the smartphone of our users. By accessing their current location we can notify them when they are near artwork they have tagged or other local artwork our users might be interested in. If users want to explore their surroundings even further, they can summon a map that contains the locations of landmarks depicted in artworks that have been discovered by our system.

#### Community
Additionally we also imagine the app as a social experience, where the users can use artworks they successfully tagged as a filter for photos they take with the camera of their smartphone. They could hereby confirm that the landmark was found. The photo could then be shared with the usual apps for sharing images.

<!-- 
### Functionality as seen by a stakeholder (0.5 page - 1 page) 
*Yuhao*
-->
### Functionality as seen by researchers and maintainers

Using this game the researchers will efficiently gain a lot of landmark location for the images in their database. Without the use of human computation to collect the information, that would be a huge amount of work that is unfeasible to do for most research facilities. Naturally it would not be completed in a short time, besides would give the high human and economic burden to designer.

With more and more users, new landmarks and information will be added into databases constantly. Problems like outages and programming errors will increase with a growing user base, so the maintainers have to solve all kinds of possible failures at any time and keep the system always stable.

The workflow of maintainers is basically very simple, as the system is designed to automate as many steps as possible. Besides maintenance of the systems the application relies on (hardware, database, ...) and bug fixing, manual spot checks that the location tags that get validated are correct are the only thing left to do.


<!-- 
### Incentivization concept (0.5 page)
*Yuhao*
 -->
### Incentivization concept

The incentivization for users to use our system is split into extrinsic and intrinsic motivation. While intrinsic motivation is preferable [@nicholson2015recipe], extrinsic motivation is a good way to attract new users.

#### Extrinsic motivation
The player with many times playing and contribution can receive indirectly feedback for the effort. For example: They can brag to their friends with their points and honor in this game. And the action significance is also very important, one can get not only the immediate validation, but also delayed validation. When users finish their game, immediately they can receive the validation from our system, for example how many landmarks have they geolocated, and how many points have gotten yet. After a couple of days the system will also inform them, which of their inputs have been took in the system. Immediate validation is the instant point rewards, and delayed validation is notifications about results show that user actions are not pointless. 

In order to users can make social interaction from an interface that is integrated into social networks such as Facebook or Twitter. We provide users a News feed posts function, our system can generate an post automatically in their social networks and which will be seen by all of their friends. By this post anyone can directly visit the game, and it can as a very import factor recruit more users, as well as motivating existing users by social incentives[@chamberlain2013methods]. 

#### Intrinsic motivation
Then the second part is intrinsic motivation, of course in this way the best motivation is the enjoyment based motivation. Firstly, users of *ARTigo* are likely to identify themselves as inherently interested in arts. Next they also can gain direct feedback from the job, immediate sense of contribution, because they know that their data will be useful in future validation. Thus People contribute information to our system, usually they are motived by personal reasons such as the desire to make a particular landmark accurate [@yang2010motivations]. On the other hand, we will set a community for all players. We want to look into community building design to improve motivation here, maybe transitioning some social motivation aspects (extrinsic) into deeper community based motivation (intrinsic).

#### Ensure long term participation
Building a community for all *landmARTigo* players is the best way to ensure users' long term participation. And we believe that notifications about successful delayed validation can make people remember this game longer. On the other hand we also adding value to the point reward system by ranking the users (maybe with special badges like “art explorer”). Because this social incentives reward players by improving their standing amongst their peers(their fellow users and friends). So tracking the user's effort can motive they compete in leaderboards, simultaneously they can see how their efforts compare to their peers [@chamberlain2013methods]. Afterwards we should pay attention to recommend this game to inherently interested people, for example architecture or art students or workers. And we have to introduce more about the worth of the system, that will help a worthy cause, this for us is not only a game, but also a very import contribution to the society.

## System design and UI elements

### System architectures (Component Diagram)

![Component Diagram (part 1)](images/component_diagram_section1.png){#fig:component-diagram-sec1 width=494px height=210.5px}

![Component Diagram (part 2)](images/component_diagram_section2.png){#fig:component-diagram-sec2 width=489px height=148.5px}

[@Fig:component-diagram-sec1] and [@fig:component-diagram-sec2] depict a high level component diagram of *LandmARTigo*'s system architecture. The system is based on API access to the existing *ARTigo* database, filtering it for artworks with tags that indicate a present landmark. These artworks are then location tagged by users, in a gamified environment. After that, the collected data is validated and processed further by different measures, explained in the following chapters.

### Algorithm for Data Aggregation

The pairwise game rounds of *landmARTigo* result in a large amount of weighted location tags. If two users pick sufficiently close locations, the tags get a weight *w* set to 1, as a primary validation step. If the users pick two different locations *w* is set to a  smaller value between 0.5 and 1 depending on the distance between the two inputs. The determined weight will be used as a multiplier during the data processing in order to consider the results of the primary validation in further steps.

This human computation process should result in a dataset of artworks, each fitted with a large number of weighted location tags. To further validate the user input and condense numerous close tags to the most likely valid locations, we decided to deploy a clustering approach.

Since we are working with a large spatial database the DBSCAN algorithm is particularly suited for our task [@sander1998density]. To find a cluster, DBSCAN starts with an arbitrary point *p* and retrieves all points within the *epsilon-radius* around *p*. If the number of points surpasses the threshold *MinPts*, *p* is considered a core point of a cluster. If no points are within the *epsilon-radius*, *p* is considered a border point and the algorithm visits the next point of the database [@ester1996density].

The DBSCAN algorithm offers several advantages for our problem:

* It contains a built in density value that we can use as a threshold for the validity of core location tags
* The density value is defined by the *epsilon-radius* and *MinPts*, therefore we are working with two simple parameters to optimise our system
* *epsilon-radius* and *MinPts* are heuristically appreciable by a k-NN approach [@dbscan2017]
* The number of clusters does not have to be specified a-priori, therefore pictures containing multiple landmarks can be considered
* The algorithm has a built in outlier detection, collecting locations that aren't contained in any core objects *epsilon-radius* as noise

We added one slight modification to the algorithm to consider the weights *w* that are collected in the primary validation process. Instead of using a constant *epsilon-radius* for each location tag, we use *w* as a multiplier on the radius. Therefore location tags with a lower weight have a smaller *epsilon-radius* and a lower chance of becoming a core object that surpasses *MinPts*, the threshold we use to determine a tags validity.

After successfully deploying the modified DBSCAN, the found clusters and their core locations are associated with the artwork that contains them and moved to our persistent storage.

From then on the found core location tags can be used to further validate user input if the primary pairwise validation fails.

### Technologies used for the implementation

##### Start-up Database and User Authentication

*landmARTigo* offers the user optional login functionalities and subsequent distribution of points as a reward. Therefore the system requires a backend for authentication and persistent data storage.

To save development time and start collecting crucial initial data, we recommend the use of *Google Firebase*. This backend-as-a-service is a unified platform for mobile and web development and offers an intuitive, well documented API. The API contains methods for authentication by email and password, as well as alternative login functionalities. *Firebase* also offers a cloud-hosted database, storing data as JSON and therefor allowing a simple key/value structure that is sufficient for the data *landmARTigo* is collecting and processing [@firebase2016]. [@Fig:data-structure] depicts a first draft of this key/value store. The data is structured into *Users* and *Artworks* on the top layer. Artwork objects are then further segmented, containing *LocationTags* and *Clusters* with their corresponding attributes.

![Basic data structure](images/datastructureHC.png){#fig:data-structure width=12cm height=7.9cm}


##### Better scalable data storage and request handling

Since the scalability of the basic *Firebase* backend is limited and the system might get demanding in API calls and grow a large user base, a dedicated server for storage, authentication and server sided data processing can become a necessity.
The *Go* programming language offers built in concurrency mechanisms and a variety of open source, third party libraries to implement an efficient, dedicated server backend for our system.

* The *Gin* web framework, by Manuel Martinez-Almeida, offers high performance HTTP request handling and is available under the MIT license (MIT) [@gingonic2018].
* *Bolt*, by Ben Johnson, is a key/value store that provides a fast and reliable database for our system and is also available under the MIT license (MIT)[@boltdb2018]. Since it uses a similar data structure as the Firebase data store, few changes have to be done on the client side when switching to the go based server.

Using a dedicated Server also offers the possibility to perform the clustering algorithm and further data processing server sided, which safes a lot of traffic.

##### Google Maps API for simple location determination

*landmARTigo* allows the users to pick the locations of Landmarks in artworks in a gamified context. We decided to use the Google Maps API to offer a fast and precise method of finding and selecting locations as tags.
The *Maps* API allows to display a map for the user, in which he can search for localities and add location tags, by simply clicking on them. Since the API has a high focus on performance [@svennerberg2010beginning], this results in a fast and fluent game experience. Considering the financing of the system, the *Open Street Maps* API[^open-street-maps] could be a valid open source alternative, especially if the system scales to a large user base.

[^open-street-maps]: <https://api.openstreetmap.org/>


### User Interfaces of the system
<!--
### User Interfaces of the system (Sketch, Paper Prototype, simple Digital Mockup) (1 - 1.5 page)
*Gregor*
-->
The user interface of our Human Computation system is in concept for a universal computer application, but primarily focused on mobile user interface elements. The functionality as previously stated is pictured in the form of a paper prototype.

![Start screen, tutorial and game screen](images/snap1.jpg){#fig:start-screen width=14cm height=7.7cm}

[@Fig:start-screen] presents the start screen, a tutorial page, and a view inside a round of the game. The start screen has a big play button to begin a new round. You can also log into the user account from here. You can reach a tutorial with the tutorial button. The tutorial is a paginated view of explanations. The big play button starts a game. The user begins a round with the first artwork they can either tag or not tag. The two main options are to either tag the landmark and move on to pinpointing the location or they can not tag the image. The second option just skips this art piece. If the user does not feel like the presented artwork is depicting a real landmark, they can tag it as potentially not containing a landmark. If many people add this remark, our system will determine, that the image(artwork) doesn't contain a landmark and will exclude the artwork for future rounds. If the user thinks they know where the depicted landmark is and pushes the button to confirm this, they are then presented with a screen to pinpoint the location.

![Pinpoint screen](images/snap2.jpg){#fig:pinpoint-screen width=14cm height=7.7cm}

[@Fig:pinpoint-screen] depicts the pinpointing screen and how the user can interact with it. They can type in the location and get instant results. They can drop a pin on the map. The user can even complete his task by a combination of both methods. If a pin has been dropped, a confirmation dialog will appear. This is to ensure that the user did not drop a pin by mistake. Confirming their location is the last step on this screen. The next artwork will appear and the cycle concludes with a round of yet undefined number of artworks (likely around 10 -- 15).

![Summary screen](images/snap3.jpg){#fig:summary-screen width=10cm height=8.4cm}

At the end of each round, a summary appears to review the artworks and actions that were done. This is shown in [@fig:summary-screen]. The user's points for each correctly determined location will be displayed next to the artwork and information about the artwork. When the user is logged in, they can reach a summary of all the rounds they played, and even get points after a round was played, if the location is confirmed at a later time. For the explorative part of the game, no prototypes exist yet. We imagine a simple notification alerting the user of a nearby landmark that is depicted in some artwork. Also another map view might be devised to let the user explore other landmarks in artworks.

Another relevant feature that needs to be depicted in our application is easily described. Our users can receive notifications when nearby a landmark that has been successfully tagged in our database. They are then presented with the corresponding artworks, if they decide to interact with the notification

## System evaluation and success criteria

After the system is implemented and established, an evaluation is required to measure its success. Thus, we need to know the limitations of this human computation system and also the criteria to classify its success.


### Limitations of the system

<!--
### Limitation of the system (0.5 page)
*Flo*
-->

First, as in every human computation system, there is the *cold start problem*. In the case of *landmARTigo*, there won't be any images with location tags at the beginning. If a user now played the game, no images with location tags in their area could be found and thus, they would just be presented random images from the ARTigo database. Most likely, the user would only know landmarks in very few of them, and playing the game would not be very entertaining.

To overcome this issue, the database should be fed with as much initial data as possible. E.g. playing the game in the cold start phase could be incentivized additionally to the methods described in [@sec:incentivization-concept] through payments, and volunteers should play a few minutes every day like in the ARTigo project [@2013artigo]. Only after enough data is collected, the game can be presented to the public and the evaluation can start.

Expectable limitations of the system after the cold start phase are mostly regarding the landmark size: Either the landmarks can be very close to each other, so the DBSCAN algorithm will merge them to one cluster, or the landmark is a very big one, e.g. a city skyline as a whole. In this case, many location tags all over the region of the city are required to represent one single cluster; or it is recognized as multiple smaller landmarks. The latter case does not have to be a misbehaviour of the system (if the users tag specific places in the city more than others, those are likely to be more important in the image), just something that has to be considered in the evaluation.


### Evaluation and success criteria

<!--
### Evaluation and success criteria (0.5 page)
*Flo*
-->

Similar as done with *Karido*, another GWAP in the ARTigo ecosystem [@2011karido], the first evaluation should be done after a period of time has passed after launching the game (so that mostly just interested ARTigo players play it) and then after the advertisement of *landmARTigo* through various channels such as the university homepage. Another long term evaluation will also gather interesting data about the usage and success; we suggest to do this approximately one year after launch.

The metrics we suggest are as follows.

##### Metrics for measuring location data accuracy

* Average DBSCAN density value of all clusters from images that have been tagged
* Number of clusters with density value above the threshold
* Average DBSCAN density value of those validated clusters

##### Metrics for measuring users' enjoyment

* Number of users
* Number of long term users (logged in users that play at least once a week for at least two months)
* Cumulated play time
* Number of users of the exploration app

<!-- TODO: Do we have to say when we consider the system a success? -->


## Future Work

### Possible extensions of the HC system

<!--
### Possible extensions of the HC system (0.5 page)
*Flo*
-->

Although our human computation system provides a way to pick locations of the landmarks that are depicted in the images, it does not let users name them. This step could be automated by an external service, though. Google provides a Maps API for reverse geocoding[^maps-reverse-geocoding], i.e. getting an address, point of interest, country, etc. for a given latitude / longitude pair. One needs to filter the results of this or a similar API to just landmarks and run it as soon as a cluster has reached the density value threshold. Special attention needs to be given to the cluster size: The cluster could represent a whole city (e.g. Munich), smaller areas (e.g. Times Square) or just buildings (e.g. Eiffel Tower; this will be the most common case). Accordingly, the name should be chosen.

[^maps-reverse-geocoding]: <https://developers.google.com/maps/documentation/geocoding/intro>

An addition to the system that could help mitigate the cold start problem would be analyzing the labels of images that were successfully tagged with a location and then automatically assigning that location to other images with similar labels, too (with low weight, because it was not entered through direct user input). Thus, more images receive location tags giving a rough estimate of landmark locations, which can act as starting points.

Another extension that could add geolocation tags automatically and thus help fight the cold start problem, is the use of natural language processing (NLP) of the artwork titles, e.g. via the Google Cloud Natural Language API[^google-cloud-nlp]. NLP is able to compute the meaning of each part of the sentence (or artwork title in this case), in specific the parts that are locations. In [@fig:google-nlp-monet], the title of a Claude Monet painting is entered in the free trial page of Google's NLP API, from which "rue Saint-Denis" is correctly recognized as a location and enhanced with a link to its Wikipedia page. From there, the geolocation data could be extracted and (again with a low weight) be added to the database.

[^google-cloud-nlp]: <https://cloud.google.com/natural-language/>

![Example painting title as NLP query](images/google-nlp.png){#fig:google-nlp-monet width=444 height=276.6}

For highly interested users, a way to enter landmark locations of chosen artworks -- instead of playing the game -- would further improve the situation. However, one needs to pay attention that one user should not be able to validate a location for an image alone, so validation through other users playing the game or reviewing those chosen artworks is still mandatory afterwards.

Once enough images are tagged with artwork locations or the "There is not a landmark" tag, *landmARTigo* could try to find similarities in the labels assigned to those images, and improve its own filter label set to find the images with landmarks in the first place.


### Interaction with other HC systems

<!--
### Thoughts on interaction with other HC system (0.5 page)
*Flo*
-->

The data that our human computation system produces, are useful on their own for the classification and categorization of artworks. However, by interaction with other human computation systems, the data are even more valuable.

Naturally, *landmARTigo* relies heavily on the *ARTigo* ecosystem; in specific the labels generated by the core game. Those are passed through a filter list to identify images that are likely to contain a landmark. As soon as a location is validated by our system, the landmark's name can be found out (see [@sec:possible-extensions-of-the-hc-system]) and this name can be passed back to the *ARTigo* system to be added as a significant label for the image. Often, the city the landmark is located in can also serve as a meaningful label.

Another human computation system that could benefit from the location data of landmarks depicted in artworks is Google's *Landmark Recognition Engine* (LRE) [@zheng2009tour]. They used photos with GPS tags and landmark data from travel websites as input data. Historic landmarks that are not existent anymore thus are also not part of these sources. Paintings of those historic landmarks on the other hand can be tagged with a location like any other artwork in *landmARTigo*. The gathered location information can be fed into LRE to increase their landmark database and -- depending on how realistic the paintings depicts the landmarks -- enable image searches for those landmarks.



##### Authors

* *Gregor Anzer*: [Abstract](#sec:abstract), [@sec:functionality-as-seen-by-a-user], [@sec:user-interfaces-of-the-system]
* *Fabian Braun*: [@sec:system-architectures-component-diagram], [@sec:algorithm-for-data-aggregation], [@sec:technologies-used-for-the-implementation]
* *Florian Edelmann*: [@sec:purpose-of-the-hc-system], [@sec:system-evaluation-and-success-criteria], [@sec:future-work]
* *Yuhao Wang*: [@sec:introduction], [@sec:human-contribution-to-the-system], [@sec:functionality-as-seen-by-researchers-and-maintainers], [@sec:incentivization-concept]
