# Lab 7: Hosting a Static Website

## Lab overview and objectives

Static websites have fixed content with no backend processing. They can contain HTML pages, images, style sheets, and all files that are needed to render a website. However, static websites do not use server-side scripting or a database. If you want your static webpages to provide interactivity and run programming logic, you can use JavaScript that runs in the user's web browser.

You can easily host a static website on Amazon Simple Storage Service (Amazon S3) by uploading the content and making it publicly accessible. No servers are needed, and you can use Amazon S3 to store and retrieve any amount of data at any time from anywhere on the web.

## Objectives

After completing this lab, you will know how to:

- Create a bucket in Amazon S3
- Upload content to your bucket
- Enable access to the bucket objects
- Update the website

## Duration

This lab requires approximately 30 minutes to complete.

## Prerequisites

This lab requires:

- Access to a notebook computer with Wi-Fi running Microsoft Windows, macOS, or Linux (Ubuntu, SUSE, or Red Hat)
- For Microsoft Windows users, Administrator access to the computer
- An Internet browser such as Chrome or Firefox

Note: This lab is incompatible with Internet Explorer 11. Use a different browser to launch this lab.

## AWS service restrictions

In this lab environment, access to AWS services and service actions might be restricted to only the ones that you need to complete the lab instructions. You might encounter errors if you attempt to access other services or perform actions beyond the ones that this lab describes.

## Accessing the AWS Management Console

1. At the top of these instructions, choose Start Lab to launch your lab.
2. A Start Lab panel opens, and it displays the lab status.
3. Tip: If you need more time to complete the lab, choose the Start Lab button again to restart the timer for the environment.
4. Wait until you see the message Lab status: ready, and then close the Start Lab panel by choosing the X.
5. At the top of these instructions, choose AWS.
6. This opens the AWS Management Console in a new browser tab. The system automatically logs you in.
7. Tip: If a new browser tab does not open, a banner or icon is usually at the top of your browser with a message that your browser is preventing the website from opening pop-up windows. Choose the banner or icon, and then choose Allow pop ups.
8. Arrange the AWS Management Console tab so that it displays alongside these instructions. Ideally, you will be able to see both browser tabs at the same time so that you can follow the lab steps more easily.


## Task 1: Creating a bucket in Amazon S3

In this task, you create an S3 bucket and configure it for static website hosting.

1. In the AWS Management Console, on the Services menu, choose S3.

2. Choose Create bucket.

3. An S3 bucket name is globally unique, and all AWS accounts share the namespace. After you create a bucket, no other AWS accounts in any AWS Regions can use the name of that bucket unless you delete the bucket. Thus, for this lab, you use a bucket name that includes a random number, such as `website-123`.

4. For Bucket name, enter `website-<123>` and replace `<123>` with a random number.

5. Public access to buckets is blocked by default. Because the files in your static website will need to be accessible through the internet, you must permit public access. First, under Object Ownership choose `ACL enabled`. Then choose `Bucket owner preferred`. Under `Block Public Access settings for this bucket`, clear the check box for `Block all public access`, and then select the box that states `I acknowledge that the current settings may result in this bucket and the objects within becoming public`.

6. Under Tags, select `Add tag` and enter the following:

- Key: `Department`
- Value: `Marketing`

You can use tags to add additional information to a bucket, such as a project code, cost center, or owner.

7. Choose `Create bucket`.

8. In the Buckets section, choose the name of your new bucket.

9. Choose the `Properties` tab.

10. You will now configure the bucket for static website hosting. Scroll to the `Static website hosting` panel and choose `Edit`.

11. Configure the following settings:

- Static web hosting: Choose `Enable`.
- Hosting type: Choose `Host a static website`.
- Index document: Enter `index.html` (Note: You must enter this value even though it is already displayed.)
- Error document: Enter `error.html`.

12. Choose `Save changes`.

13. In the `Static website hosting` panel, under `Bucket website endpoint`, choose the link.

14. You will receive a `403 Forbidden` message because you have not yet configured the bucket permissions. Keep this tab open in your web browser so that you can return to it later.

15. You have now configured your bucket to host a static website.
![AWS](https://github.com/Sohaib63/AWS-Lab-7/blob/main/Screenshot%20(57).png)
## Task 2: Uploading content to your bucket

In this task, you will upload the static files to your bucket.

1. Right-click each of the following links, and download the files to your computer:
   - index.html
   - script.js
   - style.css
   
   Ensure that each file keeps the same file name, including the extension.

2. Return to the Amazon S3 console, and choose the **Objects** tab.

3. Choose **Upload**.

4. Choose **Add files**.

5. Choose the three files that you downloaded.

6. Choose **Upload**.

Your files are uploaded to the bucket.
![AWS](https://github.com/Sohaib63/AWS-Lab-7/blob/main/Screenshot%20(58).png)

## Task 3: Enabling access to the objects

Objects that are stored in Amazon S3 are private by default. This can help your organization's data remain secure.

In this task, you will make the uploaded objects publicly accessible.

First, confirm that the objects are currently private.

1. Return to the browser tab that showed the 403 Forbidden message.
2. Refresh the webpage.
   - If you accidentally closed this tab, go to the Properties tab, and in the Static website hosting panel, choose the Bucket website endpoint link again.

You should still see a 403 Forbidden message. This response is expected! This message indicates that your static website is being hosted by Amazon S3 but that the content is private.

You can make Amazon S3 objects public through two different ways:

1. To make either a whole bucket public, or a specific directory in a bucket public, use a bucket policy.
2. To make individual objects in a bucket public, use an access control list (ACL).

It is normally safer to make individual objects public because doing so avoids accidentally making other objects public. However, if you know that the entire bucket contains no sensitive information, you can use a bucket policy.

You will now configure the individual objects to be publicly accessible.

1. Return to the web browser tab with the Amazon S3 console (but do not close the website tab).
2. Select all three objects.
3. In the Actions menu, choose Make public.
4. A list of the three objects is displayed.
5. Choose Make public.

Your static website is now publicly accessible.

Return to the web browser tab that has the 403 Forbidden message.
Refresh the webpage.
You should now see the static website that is being hosted by Amazon S3.
![AWS](https://github.com/Sohaib63/AWS-Lab-7/blob/main/Screenshot%20(59).png)
![AWS](https://github.com/Sohaib63/AWS-Lab-7/blob/main/Screenshot%20(60).png)
## Task 4: Updating the website

You can change the website by editing the HTML file and uploading it again to the S3 bucket.

Amazon S3 is an object storage service, so you must upload the whole file. This action replaces the existing object in your bucket. You cannot edit the contents of an object; instead, you must replace the whole object.

1. On your computer, load the `index.html` file into a text editor (for example, Notepad or TextEdit).
2. Find the text `Served from Amazon S3`, and replace it with `Created by <YOUR-NAME>`, substituting your name for `<YOUR-NAME>` (for example, `Created by Jane`).
3. Save the file.
4. Return to the Amazon S3 console, and upload the `index.html` file that you just edited.
5. Select `index.html`, and in the Actions menu, choose the `Make public` option again.
6. Return to the web browser tab with the static website, and refresh the page.

Your name should now be on the page.

Your static website is now accessible on the internet. Because it is hosted on Amazon S3, the website has high availability and can serve high volumes of traffic without using any servers.

You can also use your own domain name to direct users to a static website that is hosted on Amazon S3. To accomplish this, you could use the Amazon Route 53 Domain Name System (DNS) service in combination with Amazon S3.

![AWS](https://github.com/Sohaib63/AWS-Lab-7/blob/main/Screenshot%20(61).png)
![AWS](https://github.com/Sohaib63/AWS-Lab-7/blob/main/Screenshot%20(62).png)
## Submitting your work
---------------------
At the top of these instructions, choose **Submit** to record your progress and when prompted, choose **Yes**.
