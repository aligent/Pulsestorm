    /**
    * Open Source Initiative OSI - The MIT License (MIT):Licensing
    * 
    * The MIT License (MIT)
    * Copyright (c) 2009 - 2011 Pulse Storm LLC
    * 
    * Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:
    * 
    * The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.
    * 
    * THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
    */

Repository of Magento Tools from Pulse Storm LLC
==================================================	

This repository contains open source code modules and scripts to help developers work more efficiently with the Magento Ecommerce system.  They're provided free of charge by Pulse Storm LLC.  If you've found them useful you may find Pulse Storm's commercial extensions and knowledge products useful as well 

	http://store.pulsestorm.net/

You can find Pulse Storm on the web at http://www.pulsestorm.net/

IMPORTANT: Module enabling files in 

    app/etc/modules
    
default to **false**, which means the extension will not be loaded by default.  Changing this values to **true** will enable the module.    

Build Instructions
--------------------------------------------------
Building is a little janky right now, improvements are more than welcome.

The folder structure of this repository mirrors a standard Magento community edition install.  To build individual modules, simply run to the bash build scripts located at the root of the project

	$ cd /path/to/checkout
	$ ./build_developer_manual.bash
	
After running, you'll find a tar archive in the

	var/build/
	
folder.  This archive is **not** a Magento Connect module.  Rather, it's an archive that contains all the files you'll need to manually install in your system.	

Tar to Connect
--------------------------------------------------
The `magento-tar-to-connect.php` can be used to convert a plain tar archive into a Magento Connect ready package.  Usage is as follows

    $ magento-tar-to-connect.php [config.php]
    
Where `config.php` is the path to a configuration file.  Configuration files are a plain PHP `include` that returns an array in the following format

    return array(
    'base_dir'           => '/fakehome/Documents/github/Pulsestorm/var/build',
    'archive_files'      => 'Pulsestorm_Modulelist.tar',
    'extension_name'     => 'Module_List',
    'extension_version'  => '0.1.3',
    'archive_connect'    => 'Module_List-0.1.3.tgz',
    'path_output'        => '/fakehome/Pulsestorm/var/build-connect',
    
    
    'stability'          => 'stable',
    'license'            => 'MIT',
    'channel'            => 'community',
    'summary'            => 'Reports on installed Magento code modules',
    'description'        => 'This extension adds a section to the Magento Admin console which lists all install code modules.  Modules are distinct from Magento Connect packages.  A Connect package may contain a module, but it not limited to a module.',
    'notes'              => 'Added reporting on module version, moved to community code pool.',
    
    'author_name'        => 'Alan Storm',
    'author_user'        => 'alanstorm',
    'author_email'       => 'foo@example.com',
    'php_min'            => '5.2.0',
    'php_max'            => '6.0.0',
    )

This script does not (currently) support every Magento Connect package feature — instead this is a bare minimum of fields needed to get a working extension.  All files are added with the `"Magento other"` label, which allows the package directory structure to mirror an actual Magento system.

Included Modules
--------------------------------------------------
###Pulse Storm Launcher

The Pulse storm launcher provides the Magento admin console with a Quicksilver like plugin for immediate access to Magento navigation items, system configuration sections, and the Magento global search.

Original Post: http://alanstorm.com/magento_admin_navigation_launcher

###Layout Unremove

The Layout Unremove module allows you to, via Layout Update XML scripts, undo the effects of a previously executed &lt;remove/&gt; tag.

Original Post: http://alanstorm.com/magento_layout_unremove_in_local_xml

###Developer Manual

The Developer Manual extension allows you to, in real time, query your system for which action methods are available via a particular block tag.  Additional reference materials are planned. 

Original Post: http://alanstorm.com/magento_action_layout_reference

###Module List

The Module List Module provides you with a list of enabled and disable modules, as well as some simple tools for debugging your own module installation issues.  Module here refers to Magento Code Modules, which are separate from Magento Connect Extensions. 

Original Post: http://alanstorm.com/magento_list_module

###System Config Search

The system configuration search enhances the Admin Console UI and allows you to search for specific configuration fields

Original Post: http://alanstorm.com/magento_configuration_search

###X-UA-Compatible

A quick and dirty module that inserts a X-UA-Compatible meta head to force IE 9 into IE 8 compatibility mode.  Useful for users who are stuck on an older version of Magento, and/or can't manually upgrade Prototype JS. 

###Layout Viewer

Implements a query string based way to view layout information for a particular request. 

Original Post: http://alanstorm.com/layouts_blocks_and_templates

###Chaos

Inspired by the Netflix Chaos monkey, Chaos is the start to an extension which provides a framework for swapping configuration node values randomly.  Ships with code that will swap Magento in and out of flat category/product mode at random, helping your team ensure their extensions/customizations work as expected. 



Shell Scripts
--------------------------------------------------
The scripts included here are **not** the finest example of PHP shell scripting.  They're here to do a job, and that's it.  Improvements are more than welcome.


###Magento Attribute Migration Generator

This script generates a setup resource script for any existing Magento attribute.

    ./magento-create-setup.php attribute_code
    
NOTE: Must be run from the root of the Magento system with the existing attribute.    

Original Post: http://alanstorm.com/magento_attribute_migration_generator