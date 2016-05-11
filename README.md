How I did ldnode. Everything resulting from the activity is included in this repository.

Do this with sudo in /usr/local/bin/latest-ldnode

git clone https://github.com/solid/node-solid-server.git

--if needed --- (see https://davidwalsh.name/upgrade-nodejs)
npm update

sudo npm cache clean -f
sudo npm install -g n
sudo n stable

npm install -g

FYI -----

node -v
v6.0.0

Occassionally I find it helpful to go to the three horizontal slashes button (menu button) ,
then to preferences, then to advanced, then to view certificates . Then I delete anything
relating to localhost inYour Certificates, Servers, and Authorities.

This forces me to sign up again. Occassionally, I find it helpful to pull the repository again and
delete my local instance (possibly I am avoiding walking on cracks).

Use FireFox 46.0

----------
Step 0: Get Ubuntu. I chose 12.04.

Step 1. Create a folder and give it a name. I chose latest-ldnode

Step 2. clone the node-solid-server (ldnode) repository https://github.com/solid/node-solid-server.git

Step 3. Make sure you have node version 6. Per David Walsh follow these steps:

sudo npm cache clean -f
sudo npm install -g n
sudo n stable

Step 4: check your node version with node -v

Step 5. In the newly created node-solid-server folder (repository) do the following:

(A) Get a key and certificate. If doing this locally try.

openssl > genrsa 2048 > ../localhost.key
openssl req -new -x509 -nodes -sha256 -days 3650 -key ../localhost.key -subj 'CN=*.localhost' > ../localhost.crt

(B) Rename certificates and the key since they really are in pem format, (http://how2ssl.com/articles/working_with_pem_files/)
and it seems to make it work.

(C) Then run: 
solid start --port 8443 --ssl-key ../localhost.key.pem --ssl-cert ../localhost.crt.pem -v --webid

(D) when you open up https://localhost:8443 in your browser you should get something like "The site has requested you identify yourself with a 
certificate". Click cancel as long as this notice comes up. You may have other certs, but you are trying to use the one you just made. I also got a window that says "Your connection is not secure". I went ahead and
added an exception since this is the only option to go forward. This gives me an add security exception window. I chose to confirm the security
exception, but avoided the "Permanently store this exception". 

(E) If all goes well, you should get a page with create your account as the heading, and a nice blue button with create account. Hopefully you
can click it after filling in your e-mail. If you are not authorized, as you should see from the verbose option, and you see that the request failed from the browser console debugger, then repeat these steps (making sure
there is nothing related to what you have done in your browser or otherwise...git clone the repo again, clear localhost stuff from your certs).
Also, enter a name for your cert on the next screen and click the blue button below.

(F) If you get to the "You're all set!" page simply reload the browser, and you should see your data loaded with the default warp file browser.

