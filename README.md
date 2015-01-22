# Entityclassifier.eu Stand-Alone Plugin for GATE #

This is a GATE **stand-alone** plugin for the Entityclassifier.eu NER system. You can use it perform Named Entity Recognition over English, German and Dutch written texts. All resources you need for entity spotting, disambiguation and classification are provided with the plugin. If you want, you can use the **light** version of the plugin which is communicating with our REST API endpoint. Using this plugin you can perform:

* ***Entity Spotting*** - each detected named entity in the text will be marked with ```NamedEntity``` annotation.

* ***Entity Disambiguation*** - each spotted entity is further disambiguated with a an URI from the *DBpedia namespace*. E.g. http://dbpedia.org/resource/Prague for the entity Prague.

* ***Entity Classification*** - for each disambiguated entity we provide set of types represented as *DBpedia instances* or *DBpedia Ontology* types. When using the plugin you can set the ```typesFilter``` parameter to filter out only types as DBpedia instances, DBpedia Ontology types, or both. The possible parameter values are:
    * **dbo** - filter only DBpedia Ontology types
    * **dbinstance** - filter only types defined as DBpedia instances
    * **all** - the entity types can be either DBpedia Ontology clases or DBpedia instances


### How to start using it? ###

#### Steps: ####


1. **Clone the repository in your GATE plugins directory.** In MAC OS the plugins directory can be found in ```/Applications/GATE_Developer_7.1/plugins```

    ```
    git clone https://m1ci@bitbucket.org/entityclassifier/entityclassifier-gate-stand-alone-plugin.git
    ```

2. **Run the build script found in the script folder.** It will download all required datasets, compile and prepare all required configuration files. BTW, grab a coffee or something, it will take some time ;)

    ```
    sh build.sh
    ```

3. **Download and install GATE.**
You can download it from http://gate.ac.uk/download/


4. **Start GATE and enable the plugin in the CREOLE plugin manager.** Search for Entityclassifier.eu and select load now and load always.

5. **Create a corpus pipeline.**

    * Document Reset PR
    * ANNIE English Tokeniser PR
    * ANNIE Sentence Splitter PR
    * ANNIE POS Tagger PR
    * JAPE Transducer PR - with a JAPE grammar which will perform named entity spotting. For English use the ```en_entity_extraction-v1.jape```. We also provide grammars for entity spotting for German and Dutch. The grammars are located in ```data/entity-extraction-grammars```
    * Entityclassifier.eu Stand-Alone PR - create an instance of classifier processing resource and add it at the end of the pipeline. When instantiating you can specify the language of the text on which you will run named entity recognition.

6. **Create a document corpus and run the pipeline.**

7. **Check the results!** - the spotted entities are annotated as ```NamedEntity``` annotations. Each entity has a ```disambiguation URI``` which is encoded as annotation feature ```itsrdf:taIdentRef=...```. Each assigned type is also present as annotation feature in the form of ```rdf:typeX=...```

![entityclassifier-sa-gate-plugin-ss-1.png](https://bitbucket.org/repo/dAnKEK/images/3433177732-entityclassifier-sa-gate-plugin-ss-1.png)

***Enjoy discovering entities!***



If you need any help/support with the plugin free to contact us. Bugs please report as issues to this repository.

License
------

Licensed under the [GNU General Public License Version 3 (GNU GPLv3)](http://www.gnu.org/licenses/gpl.html).

Copyright (c) 2014

* Milan Dojchinovski - <milan.dojchinovski@fit.cvut.cz>

* Tomas Kliegr - <tomas.kliegr@vse.cz>