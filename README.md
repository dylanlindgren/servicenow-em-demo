# ServiceNow Engagement Messenger Demo

Engagement Messenger is a new feature of the Quebec release of ServiceNow. It allows you to embed a messenger-like popup inside any website to interact with ServiceNow features, such as browsing knowledge, creating a case, and interacting with Virtual Agent.

Given it is meant for external websites, this app was created to assist you in simulating this experience whist using Engagement Messenger.

![ServiceNow Engagement Messenger Demo](images/banner.png)

### Pre-requisites
* Install Git from [https://git-scm.com/downloads](https://git-scm.com/downloads)
* Install Docker from [https://docs.docker.com/get-docker](https://docs.docker.com/get-docker)

## Getting the Demo

### Open Terminal

Open a Terminal window. It should open in your home directory by default, but you can run the command `cd ~/` if it hasn't.

### Clone this Repository

Execute the following command to clone this repository into a folder

```
git clone https://github.com/dylanlindgren/servicenow-em-demo.git
```

You will now have the `servicenow-em-demo` folder inside your home directory.

## Preparing the Demo

### 1) Take a Screenshot

Inside the  `servicenow-em-demo` folder you will see a `background.png` file. This is the file that is used as the background image of the demo page.

You will need to take a screenshot of the portal/website that you are proposing Engagement Messenger be embedded into — for example, the support page of a customer's existing website.

Firefox has a great tool for taking screenshots, easily allowing you to take one of the entire scrolling area of the page. You can find instructions on how to do this here: [https://www.wikihow.com/Take-a-Screenshot-on-Firefox](https://www.wikihow.com/Take-a-Screenshot-on-Firefox).

![Firefox's screenshot function](images/screenshot.png)

### 2) Set Your Background Image

Once you have your screenshot, replace the `background.png` file inside this directory with it.

### 3) Configure Your Hosts File

The demo will be running from your local computer. To make the demo especially impactful, you might want to modify your hosts file so that page looks like that of the customer.

For example, for *Apple* you might want the demo to appear like it's coming from *applesupport.com*.

In terminal, open your hosts file for editing using the following command:

```
sudo nano /etc/hosts
```
Add a line at the bottom to resolve *applesupport.com* to *127.0.0.1* (your computer)

```
127.0.0.1       applesupport.com
```

![Hosts file](images/hosts.png)

Press `CTRL + O` to save the file, and then `CTRL + X` to quit.


### 4) Configure ServiceNow

There are a number of steps required on the ServiceNow instance which are all documented on the ServiceNow Docs website.

1. [Configure an Engagement Messenger module](https://docs.servicenow.com/bundle/quebec-customer-service-management/page/product/customer-service-management/task/create-engagement-messenger-module.html) - Take a note of the Sys ID of the Module as we will use this in the next step.
2. [Configure CORS rule for Engagement Messenger](https://docs.servicenow.com/bundle/quebec-customer-service-management/page/product/customer-service-management/task/create-cors-for-rest-api-ec.html) - Set this to the full address we will be accessing the demo on plus the port number `8084`. For example: `http://applesupport.com:8084`
3. [Create HTTP response headers for Engagement Messenger](https://docs.servicenow.com/bundle/quebec-customer-service-management/page/product/customer-service-management/task/create-http-response-headers-for-ec.html) - You can set this value to `frame-ancestors 'self' *`
4. [Configure the Virtual Agent System Properties](https://docs.servicenow.com/bundle/london-performance-analytics-and-reporting/page/administer/virtual-agent/task/embed-va-standalone-client.html) - You can set this vaule to `frame-ancestors 'self' *`

### 5) Configure the Demo

Open the `.env` file inside the `servicenow-em-demo` folder. By default it will look like this:

```
SN_EM_MODULE_ID=60c794c3db862010b7c8dacbd39619fe
SN_EM_INSTANCE_NAME=dl3
```

Just replace these with the Sys ID of your Engagement Messenger module, and the name of your instance and save the file.

## Running the Demo

Simply run the following command in your `servicenow-em-demo` folder to **start** the demo:

```
docker-compose up -d
```

To **stop** the demo, from your `servicenow-em-demo` folder run the following commmand:

```
docker-compose down
```