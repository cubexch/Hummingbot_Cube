# Hummingbot x Cube 🧊

We recommend installing Hummingbot using Docker if you want the simplest, easiest installation method and don't need to modify the Hummingbot codebase.

Installation Process

### 1. Install Docker Compose
   
Hummingbot uses [Docker Compose](https://docs.docker.com/compose/), a tool for defining and running multi-container Docker applications.

The recommended way to get Docker Compose is to install [Docker Desktop](https://www.docker.com/products/docker-desktop/), which includes Docker Compose along with Docker Engine and Docker CLI which are Compose prerequisites.

After installing Docker Desktop, verify that Docker Compose is installed correctly by checking the version:
```
docker compose version
```
The output should be: ```Docker Compose version v2.17.2``` or similar.

### 2. Clone Repo

Enter the following commands in Bash/Terminal to clone the Hummingbot Github repo and enter the root folder:
```
git clone https://github.com/hummingbot/hummingbot.git
cd hummingbot
```
### 3. Pull Image

The ```docker-compose.yml``` file in the root folder provides a basic configuration for launching an instance.

You will be able to modify this file and uncomment lines in order to automatically enter your pasword and start strategies. For now, we can use it as-is.

Run the following command to pull the image and start the instance:
```
docker compose up -d
```
After the images have been downloaded, you should see the following output:
```
[+] Running 1/1
 ⠿ Container hummingbot  Started
```

### 4. Attach to Instance

The``` -d``` flag runs Hummingbot in detached mode. Attach to it by running the command:
```
docker attach hummingbot
```

You should now see the Hummingbot welcome screen:
![hummingbot_home](https://github.com/nickFNY/Hummingbot_Cube/assets/63250024/305aeff9-0ad0-4e08-addc-c5148dd210c5)

For Advanced Strategy and Configurations, please see the Hummingbot Docs: https://hummingbot.org/installation/docker/#advanced-configurations


## Conenct to Cube 

### Generate API Keys

1. Go to [Cube Exchange](https://www.cube.exchange/) and log in or create a new account.
2. Open the API Key page by clicking over the profile icon on the top right corner and go to the Setting/API page at https://www.cube.exchange/settings/api.
3. Click on the _**Add another API**_ button
![image](https://github.com/nickFNY/Hummingbot_Cube/assets/63250024/93919093-7766-4db5-ae4c-a4ecee745eb6)
4. Choose your account, select _**WRITE**_ permission and click _**Create API Key**_
5. Copy your API keys and store them somewhere safe.
6. Go to Subaccounts page and copy your _**Subaccount ID**_ number. You will need this to connect to Hummingbot.
![image](https://github.com/nickFNY/Hummingbot_Cube/assets/63250024/f862a230-4a95-48d6-8965-4e9cb64ebe14)
7. Now, you have created API keys for your Cube Exchange!

### Add Keys to Hummingbot
From inside the Hummingbot client, run ```connect cube```:
```
>>> connect cube

Enter your Cube Exchange API key >>>
Enter your Cube Exchange secret key >>>
Enter your Cube Exchange Subaccount ID >>>
Enter your Cube environment (live or staging) >>>
```
If connection is successful:
```
You are now connected to cube
```

### Rate Oracle
The connector comes with its own rate oracle implementation. You can use it by using the folllowing command:
```
config rate_oracle_source cube
```
Make sure to set global token name to ```USDC``` as ```USDC``` is the main quote token for trading on Cube Exchange
```
config global_token.global_token_name USDC
```

### Strategies 

Once connected, you can run various trading strategies on Cube

Strategies: 
- V1: https://hummingbot.org/v1-strategies/
- V2: https://hummingbot.org/strategies/
- Scripts: https://hummingbot.org/scripts/

### Example: Pure Market Making Strategy 

To deploy a pure market making strategy on Cube, 
```
>>> Create

What is your market making strategy >>> pure_market_makng 

Enter your maker spot connector >>> cube 

Enter the token pair you woudl like ot trade on cube (e.g. SOL-USDC) >>> SOL-USDC

How far away from the mid price do you want to place the first bid order? (Enter 1 to indicate 1%) >>> .1

How far away from the mid price do you want to place the first bid order? (Enter 1 to indicate 1%) >>> .1

How far away from the mid price do you want to place the first ask order? (Enter 1 to indicate 1%) >>> .1

How often do you want to cancel and replace bids and asks (in seconds)? >>> 10 

What is the amount of SOL per order? >>> 5

Enter a new file name for your configuration >>> conf_pure_mm_1.yml
```
Your strategy has been created. To start, simply run: ```start```
