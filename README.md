# chucknorris
Sample Splunk SOAR (formerly Phantom) app for the Chuck Norris API

Command format for creating the TAR file
----------------------------------------

Modify the exclude file and add any files or directories you don't want in the TAR file

```shell
cd /home/phantom/app/chucknorris
tar --exclude-from phchucknorris/exclude_files.txt -zcvf chucknorris.tgz phchucknorris
```


Instructions for creating a container and artifact
--------------------------------------------------

From the Splunk SOAR user interface (UI) naviate to Administration -> User Management -> Users and edit the user `automation`.  You need to show the token or set a new token.

```json
{
  "ph-auth-token": "*********",

  "server": "https://54.237.22.123"
}
```

Change the `Allowed IPs` to ***any*** or the IP address from where you are initiating the program.

From the Phantom CLI, create two environment variables.

```shell
export PH_AUTH_TOKEN=2adnymvMJMredactedHOM+xBGUNs1wEk=
export PH_SERVER=54.237.22.123
```

Download the code
-----------------

```shell
mkdir artifact
cd artifact
curl https://raw.githubusercontent.com/joelwking/Phantom-Cyber/master/REST_ingest/PhantomIngest.py -o PhantomIngest.py
```

Run the Python program
----------------------

Download and run this program to create events in Splunk SOAR so the app can be run against an artifact.

```shell
phenv python
```
Modify, and cut-n-paste the following into your Python interpreter.

```python
import PhantomIngest as ingest
import os
p = ingest.PhantomIngest(os.getenv('PH_SERVER'), os.getenv('PH_AUTH_TOKEN'))
kontainer = {'name': 'Voltaire', 'description': 'French Enlightenment writer, historian, and philosopher.', 'label': 'events'}
container_id = p.add_container(**kontainer)
art_i_fact = {"name": "François-Marie Arouet", "source_data_identifier": "IR_3458575"}
cef = {'sourceAddress': '192.0.2.1', 'sourcePort': '6553', 'sourceUserId': 'voltaire@example.net'}
meta_data = {}
artifact_id = p.add_artifact(container_id, cef, meta_data, **art_i_fact)
print(p.status_code, container_id, artifact_id)
```

Provided you have a status code of `200`, navigate to the Splunk SOAR UI and a new event should appear.

Test the app
------------

Select the Event and Artifact, and `Run Action`. Select `By App`, select the ***chucknorris*** app. Then select the **action** of `get_category` or `get_random`.

If the app run is successful, you can ***Download the JSON*** or ***Open in new window***.

Author
------
Joel W. King @joelwking