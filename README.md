# CKEditorForMendixLite

This extended version of the CKEditorForMendix widget contains all the basic features and in addition allows the user to configure the widget to activate tracking and managing textual changes. It uses the Lite plugin to do this. Fot this to work properly it is ammended to do two things: 
1) enabeling and disabeling LITE
2) enabeling the control elements in the CKEditor interface

sub 1) From the LITE <a href="http://www.loopindex.com/lite/docs/" target="_blank">documentation</a>documentation ("http://www.loopindex.com/lite/docs/"):   

	Add the lite plugin to ckeditor. The simplest way to do this is by adding the following line to ckeditor's config.js:
		config.extraPlugins = 'lite'
	
	Optionally include lite-interface.js in your source, so you can use the various constants defined in it rather than string literals.
	See the documentation for all the configuration options.
	
	The LITE plugin is automatically activated after you install it and edit config.js as described above. For the full details of tweaking the loading process, toolbar commands, users and more, see the documentation. The LITE plugin exposes a wide range of methods, events and properties for controlling and reporting the tracked changes. see the documentation for details.
	LITE tracks only text insertion and deletion. Other changes, such as style edits, are not tracked.
	LITE has been tested on Firefox 15+ and Chrome 13+. Support for MSIE 9+ is not guaranteed, although the current version seems to work on it.
		
In the widget this is implemented in the following way:
	
	Added in CKEditorForMendix.js
	
PLUGIN DEFINITIONS
	
	 ckeditorPlugins: [
            "divarea",
            "mendixlink",
            "tableresize",
            "oembed",
            "widget",
            "maximize",
            "lite"
        ],
		
GET PLUGINS (after the wordcount option)

            if (this.countPlugin) {
                plugins.push("wordcount");
            }
            
            if (this.trackChanges) {
                plugins.push("lite");                
            }

TOOLBAR definition (after Others)
		if (this.toolbarOthers) {
                this._settings[this.id].config.toolbarGroups.push({
                    name: "others"
                });
            }

		if (this.showChanges) {
                this._settings[this.id].config.lite.commands = ["lite-toggletracking",  "lite-toggleshow", "lite-acceptall", "lite-rejectall", "lite-acceptone",  "lite-rejectone",  "lite-toggletooltips"];

                this._settings[this.id].config.toolbarGroups.push({
                    name: "lite"
                });
            }
			
2) adjusting the Editor.XML for the controlelements
	
Added after the OTHERS item
	
		<property key="trackChanges" type="boolean" required="true" defaultValue="true">
            <caption>Track Changes</caption>
            <category>Document</category>
            <description>Activate Track Changes without showing the toolbar.</description>
        </property>
        <property key="showChanges" type="boolean" required="true" defaultValue="true">
            <caption>Tracking Tools</caption>
            <category>Document</category>
            <description>Show the Track Changes toolbar.</description>
        </property>          
					
3) configuratie LITE plugin
	Optional configuration of the Lite plugin (marking colour etc) is possible, but not (yet) attemted
