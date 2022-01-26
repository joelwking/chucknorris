# chucknorris
Sample Splunk> SOAR (formerly Phantom) app for the Chuck Norris API

This app enables process and documentation validation for creating an app on Splunk> SOAR.

Update date and version
-----------------------
Update the JSON file, verify the version and update time are correct.

```json
    "app_version": "1.0.0",
    "utctime_updated": "2022-01-26T20:15:03.075859Z",
```

Compile the app
---------------
Compile the Chuck Norris app, and install it.

```
[phantom@appdev phchucknorris]$ phenv python /opt/phantom/bin/compile_app.pyc -i
cd'ing into ./
Validating App Json
    App json found at ./chucknorris.json
  Validating App Json
  Validating actions
    test connectivity
      No further validation coded for "test connectivity" action
    get random
      Done
    get category
      Done
Compiling: ./__init__.py
Compiling: ./chucknorris_connector.py
Compiling: ./chucknorris_consts.py
Installing app...
  Creating tarball...
  ..//home/phantom/app/chucknorris/phchucknorris.tgz
  Calling installer...
  Success
Done
```

Command format for creating the TAR file
----------------------------------------
Modify the exclude file and add any files or directories you don't want in the TAR file

```shell
cd /home/phantom/app/chucknorris
tar --exclude-from phchucknorris/exclude_files.txt -zcvf chucknorris.tgz phchucknorris
```

The output is as follows:

```
[phantom@appdev chucknorris]$ tar --exclude-from phchucknorris/exclude_files.txt -zcvf phchucknorris.tgz phchucknorris
phchucknorris/
phchucknorris/__init__.py
phchucknorris/chucknorris.png
phchucknorris/chucknorris_connector.py
phchucknorris/chucknorris_consts.py
phchucknorris/chucknorris_dark.png
phchucknorris/exclude_files.txt
phchucknorris/readme.html
phchucknorris/test_jsons/
phchucknorris/test_jsons/category.json
phchucknorris/test_jsons/random.json
phchucknorris/test_jsons/test.json
phchucknorris/chucknorris.json
```

>Note: verify the excluded files were actually excluded.

```
[phantom@appdev chucknorris]$ more phchucknorris/exclude_files.txt 
.git*
.vscode*
phchucknorris/__pycache__
```

Author
------
Joel W. King @joelwking