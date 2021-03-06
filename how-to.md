---

copyright:
  years: 2017
lastupdated: "2017-09-11"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# Manage your CDN

Learn how to manage your CDN configuration by following these guidelines.
 
## Getting the CDN to running status

Once you've created a CDN, it appears on your CDN dashboard. Here you'll see the name of your CDN, the Origin, the Provider, and the status.  

 ![Mapping list screenshot](images/mapping_list_cname.png)

1. After you've ordered a CDN, you'll need to configure the **CNAME** with your DNS provider. Most DNS providers can give you instructions on setting or changing the CNAME.
   
   * During this time, your CDN's status will show as **CNAME Configuration**. Check with your DNS provider to find out when the changes will become active.

   ![CNAME config](images/cname-config.png)  
   
2. Any time after you've configured the CNAME with your DNS provider, you may check the status by selecting **Get Status** from the overflow menu to the right of the CDN's status.
   
  ![CNAME getStatus](images/cname-getstatus.png)  
    
3. When the CNAME chaining is complete, the account status changes to *RUNNING*, and the CDN is ready to use.
   	  
Congratulations! Your CDN is now running.  
	  
## Stopping CDN
A CDN can be stopped only when in 'Running' status. 

1. Click 'Stop CDN' from the Overflow menu (3 vertical dots to the right of the CDN status).
 ![Overflow menu](images/stop_cdn.png)

2. A larger dialog window appears, asking to confirm that you want to stop the service. Select **Confirm** to Proceed.
  
3. After about 5 to 15 seconds, the status should change to 'Stopped'


## Starting CDN
A CDN can be started only when in 'Stopped' status
1. Click 'Start CDN' from the Overflow menu, which appears as three dots to the right side of the CDN row.
 ![Overflow menu](images/start_cdn.png)

2. A larger dialog window appears, asking to confirm that you want to start the service. Select **Confirm** to Proceed.

3. If the action was successful, a dialog box appears in the upper right corner of your screen, letting you know that it was successful, along with the time.
  
4. This will change the Status to 'CNAME Configuration'

5. Click 'Get Status' from Overflow menu. This will change the status to 'Running'. And CDN will become operational.

## Deleting CDN

To delete a CDN follow the steps below:
**NOTE**: Selecting `Delete` from the overflow menu only deletes the CDN; it will not delete your account.

1. Click 'Delete' from the overflow menu.

 ![Delete CDN Overflow menu](images/delete_cdn.png)

2. A larger dialog window appears, asking to confirm that you want to delete. Click **Delete** to Proceed

3. This will change the status to 'Deleting'. Click 'Get Status' from overflow menu. This will remove the row from the CDN list.

## Setting content caching time using "Time To Live"

After your CDN is running, you can set your content caching time using Time To Live (TTL). The Time To Live for a particular file or directory path indicates how long that content should be cached. When you created the CDN Mapping, a default global TTL of 3600 seconds was created. 

1. On the CDN page, select your CDN, which will take you to the **Overview** page.

2. You can adjust the time using the arrows or by entering a new time. The time value is specified in seconds. For example, 3600 seconds is equal to 1 hour. The smallest value for `timeToLive` that can be chosen is 30 seconds, while the largest is 2147483647 seconds. Select the **Save** button to set the content caching time. 

  ![Adding ttl](images/adding-path.png)

3. After saving, you can **Edit** or **Delete** the TTL setting using the overflow menu options. (**NOTE**: The Path for TTL cannot be changed. If the Mapping path is changed, the TTL path will update automatically.)

  ![Edit or delete ttl](images/edit-delete-ttl-setting.png)  
	
  * When the content matches multiple rules, the most recently added configuration will take precedence.
  
  * TTL values can be set only for a specific file name or directory. Regular expressions are not supported, because they may create unpredictable behavior.
	
## Adding Origin Path details

When your CDN is in *CNAME_Configuration* or *Running* status, you can add Origin Path details. You can choose to provide content from multiple Origin Servers. For example, photos can be delivered from a different server than videos. The Origin can be based upon a Host Server or Object Storage. 

Note: CDN will make a URL transformation for the origin server. For example, if origin xyz.example.com is added with path /example/\* when a user opens the URL www.example.com/example/* , the CDN edge server will retrieve the content from xyz.example.com/*

1. On the CDN page, select your CDN, which takes you to the **Overview** page.
	
2. Select the **Origins** tab, then select the **Add Origin** button.
	
3. You *must* provide a path. The path *must* start with the CDN path as the prefix, if the CDN was created with a path. 
   For example, if the CDN was created with a path of '/examplePath' the path for the Origin must start with prefix  '/examplePath/'

4. Select either **Server** or **Object Storage**.
	
   ![Origins add origin](images/add-origin.png)
		
  * If you selected **Server**, enter the Origin server address as IPv4 address or the _hostname_. It is recommended to provide _hostname_ and provide a Fully Qualified Domain Name (FQDN). Provide an HTTP port, an HTTPS port, or both, depending on which protocol you selected during CDN creation.
	
  ![Add origin server](images/add-origin-server.png)
	
  * If you selected **Object Storage**, provide the Endpoint, Bucket name, and HTTPS port. Optionally, specify the file extensions that can be used in the CDN service. If nothing is specified, all file extensions are allowed.
	
  ![Add origin object storage](images/add-origin-object-storage.png)

Note: The Protocol and Port options shown by the UI will match what was selected during ordering the CDN. For example, if **HTTPport** was selected as part of ordering a CDN, only the **HTTPport** option will be shown as part of Add Origin.

5. Select the **Add** button to add your Origin Path.

  **Note**: When you provide file extensions for an Object Storage origin path, the TTL setting that has the same URL as the origin path will be scoped to include all files that have those specified file extensions. For example, if you create an origin path of "/example" and specify file extensions of "jpg png gif", the TTL value of the TTL path "/example" will have a scope that includes all JPG/PNG/GIF files under the "/example" directory and its sub-directories.

6. After adding, you can  **Edit** or **Delete** the Origin using the overflow menu options.

  ![Edit or delete Origin](images/edit-delete-origin.png)



## Purging Cached Content

After your CDN is running, you can purge cached content from the Vendor's server.  

1. On the CDN page, select your CDN, which takes you to the **Overview** page.
	
2. Select the **Purge** tab.

	![Purge page](images/purge_tab.png)
	
3. Enter standard unix path syntax to indicate which file you would like to purge, then select the **Purge** button. Purge is only allowed for a single file at this time.

4. After purging, the activity is listed under **Purge Activity**. You can **Redo purge** or **Favorite** the path using the overflow menu options.

	![Purge activity](images/purge-activity.png)
	
   **NOTE:** If there are more than 15 purges, Purge Activity is trimmed every 15 days automatically.
	
## Updating CDN Configuration details

After your CDN is running, you can update CDN configuration details.

1. On the CDN page, select your CDN, which takes you to the **Overview** page.

2. Select the **Settings** tab. Your CDN configuration details are displayed.

  For **Object Storage**, following fields can be changed: 
   * Endpoint
   * Bucket name
   * HTTPS Port
   * Allowed file extensions
   * Serve Stale Content
   * Respect Headers

  For **Server**, following fields can be changed: 
   * Origin server address
   * HTTP/HTTPS Port
   * Serve Stale Content
   * Respect Headers

3. Update the **Origin** or **Other Options** details if needed, then click the **Save** button in the bottom right corner to update your CDN configuration details.

   ![Save button](images/save-button.png)


## Configure IBM Cloud Object Storage for CDN

To make use of objects stored in IBM Cloud Object Storage, you must set the value of the "acl" property (that is, the access control list) for each object in your bucket for "public-read" access. 

Please refer to the Tools section IBM Cloud Object Storage Developer Center (https://developer.ibm.com/cloudobjectstorage/) to install any neccessary clients or tools. This guide assumes you have installed the official AWS command line interface, which is compatible with IBM Cloud Object Storage S3 API.

The example code below shows how to set "public-read" access for all the objects in your bucket, using the command line interface.

```
$ export ENDPOINT="YOUR_ENDPOINT"
$ export BUCKET="YOUR_BUCKET"
$ KEYS=( "$(aws --endpoint-url "$ENDPOINT" s3api list-objects --no-paginate --query 'Contents[].{key: Key}' --output text --bucket "$BUCKET")" )
$ for KEY in "${KEYS[@]}"
  > do
  >   aws --endpoint-url "$ENDPOINT" s3api put-object-acl --bucket "$BUCKET" --key "$KEY" --acl "public-read"
  > done
```
