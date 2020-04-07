# smsmap
sms to mapping tool, as simple coronavirus support

This is just a placeholder for the main site on sourceforge
https://sourceforge.net/p/smsmap/code/ci/master/tree/
or simple debian package also available.

Description

SMS to Log and Clustered Web Map
Takes SMS messages containing a postcode and a message and logs them in a database. Displays colour coded clusters on Open Street Map. I have no idea whether this works on Windows, developed on Linux Mint and works pretty well on an old desktop, that’s the ‘idea’. 
1. Send an SMS with postcode and message to an SMS -> API service (Plivo, in my case, but can adapt, reasonably easily). see and modify the convert_to_plivo_format function, probably a couple of lines of code.

2. Report is logged, appears on map and is clustered, idea is to provide infrastructure and optimise (clustering) informal help calls, find hotspots in a local area. Probably, attach to a ticketing system also. It’s Perl, Mojolicious, current sqlite (though DBix so I could upgrade to Postgres) and the currently unpackaged core (without counting libraries!) is very small. Basically it’s an ‘anti app’ application, since many people don’t have smart phones, some many don’t have broadband and the libraries are closing.

For the moment, find me @hughbarnard on Twitter for help. This is alpha-quality, so if you can improve that’s welcome, also.

1. Needs Perl and Mojolicious also DBIx::Class, IO::Socket::IP, Socket (it uses websockets to display data). All those via CPAN or apt install
2. Testing script that will need to be adapted for non-UK in sms_map/t use prove -lv
3. For UK needs to load status.db translate table with UK postcodes and long/lat via https://www.getthedata.com/open-postcode-geohttps://www.getthedata.com/. Non UK, YMMV if I find out I’ll add
4. For example, loading the table from csv $ sqlite3 status.db sqlite> .mode csv sqlite> .import postcode.csv translate sqlite> .exit
5. Adjust sms_map.conf to point to the database. Other settings are for postcode parsing too
6. The SMS in this version is delivered from Plivo: https://www.plivo.com/, if Twilio or (locally) Gammu + dongle is used, a few adjustments need to be made
7. Adjust map centre in templates/index.html.ep for your locality
8. cd sms_mapscript and morbo sms_map should start listening and displaying on port 3000. Use NAT settings on the router to serve it to the outside. Again, this can be run on a not-very-powerful PC in-house.
