For deploying static websites with the serverless framework do the following:

<ol>
<li>Verify your E-Mail in AWS SES. This will be the sender! 
  
<li>If not installed, then install serverless framework: </li>
<code>npm install -g serverless</code>

<li>Create the service in a new folder: </li> 
<code>serverless create -u https://github.com/albertschwarzkopf/serverless-static-website-with-contact-form -n serverless-static-website-with-contact-form</code>

<li>Go in the new directory.</li>

<li>Install the S3 sync plugin:</li>
<code>serverless plugin install -n serverless-s3-sync</code>

<li>Change the service name in serverless.yml

<li>Overwrite your static files and folders into the static directory.
  
<li>Deploy your Stack and put you Email-adress here. This will be used as Sender in SES:</li>
  <code>serverless deploy --email youremail@example.de -v --region eu-west-1</code>

<li>Write the given Api-Endpoint in the Contact-Html-file:</li>
<code>new_endpoint="var URL "="\"`sls info --verbose | grep POST | sed 's/  POST - //'`\";"</code>
<br>
<code>old_endpoint=`grep "var URL" static/contact/contact.html`</code>
<br>
<code>sed -i "s|$old_endpoint|$new_endpoint|g" static/contact/contact.html</code>

<li>You have to sync again the files, because you have changed the contact form:</li>
<code>serverless deploy --email youremail@example.de -v --region eu-west-1</code>
</ol>

Hints:
<ul>
<li>Take a short name without uppercase characters for serice, because it ist used by default for Bucket-Name and IAM-Role.</li>
<li>If you want to save the sent messages in DynamoDB when you can activate this feautre in serverless.yml</li>
</ul> 
<br>
Todo:
<li>new_endpoint="var URL "="\"`sls info --verbose | grep POST | sed 's/ POST - //'`\";"
<li>old_endpoint=`grep "var URL" static/contact/contact.html`
<li>sed -i "s|$old_endpoint|$new_endpoint|g" static/contact/contact.html
