stardict.js
==========

JavaScript library for handling dictionaries in StarDict format.

This project is put on ice till late February 2014! Please contact me if you have plans to work on it in the meantime. Major restructuring plans are already on paper and I might have to think these plans over if somebody comes up with great new ideas.
---

The code depends on two further javascript libraries, namely:

- https://github.com/tuxor1337/dictzip.js  
- https://github.com/augustl/js-inflate

referred to in the code as "DictZipFile" and "JSInflate.inflate" respectively.

Example Code
---

    var dict = new StarDict();
    
    $("input[type=file]").change(function(evt) {
        dict.onsuccess = (function (theDict) {
            return function () {
                wid = theDict.lookup_term("cat")[1];
                theDict.lookup_id(wid, function (data_arr) {
                    data_arr.forEach(function (d) {
                        type = d[1];
                        data = d[0];
                        console.log("type=" + type);
                        console.log("string=" + data);
                    });
                });
            };
        })(dict);
        
        /* We are expecting a list of files here, containing at least an *.ifo,
         * an *.idx and a *.dict (or *.dict.dz) file.
         * Optionaly supported are a *.syn file as well as additional resources
         * in the form of a tuple of *.rifo/ridx/rdic files.
         * As a second argument, we can provide another list of files which contains
         * the contents of the subdirectory "res".
         */
        dict.load(evt.target.files);
    });


Further reading
---

Format documentation (original documentation is lost): http://code.google.com/p/babiloo/wiki/StarDict_format
 
Python lib: http://code.google.com/p/pytoolkits/source/browse/trunk/utils/stardict/StarDict.py  
Java lib: http://code.google.com/p/toolkits/source/browse/trunk/android/YAStarDict/src/com/googlecode/toolkits/stardict/StarDict.java
