Ubuntu OS

Step1  
//Install node.js,the node .js version is v8.11.3. and  npm version 5.6.0  
```curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash -```  
```sudo apt-get install -y nodejs```  

Step2  
//Install bitcoinABC's bitcoind (version is 0.17.2) 
```sudo apt-get install software-properties-common```  
```sudo add-apt-repository ppa:bitcoin-abc/ppa```  
```sudo apt-get update```  
```sudo apt-get install bitcoind```  

Step3  
//Install bitcore  
```sudo apt-get install libzmq3-dev build-essential```  
```sudo npm install -g --unsafe-perm=true bitcore```

Step4  
//bitcore create bitcoin cash project  
```cd ~```  
```bitcore create bitcoin-cash-node```  
```cd bitcoin-cash-node```  
```npm install bitcore-lib-cash --save```    
```npm uninstall bitcore-lib  --save```  
```npm install insight-api insight-ui --save```   
```npm install```   

Step5  
//edit bitcode-node.json  
```cd ~/bitcoin-cash-node```  
```vi bitcore-node.json```
```
{  
  "network": "livenet",  
  "port": 3001,  
  "services": [  
    "bitcoind",  
    "web",  
    "insight-api",  
    "insight-ui"  
  ],  
  "servicesConfig": {  
    "bitcoind": {  
      "spawn": {  
        "datadir": "[somewhere you want to sync and store the data]",  
        "exec": "bitcoind"  
      }  
    }  
  }  
}  
```

Step6(options)  
//Install pm2  
```cd ~```  
```sudo npm install pm2 -g```  
//If the server reboot,pm2 will auto restart.  
```pm2 startup```  
```sudo env PATH=$PATH:/usr/bin /usr/lib/node_modules/pm2/bin/pm2 startup systemd -u ubuntu --hp /home/ubuntu```  
```pm2 save```  

//if you install pm2 please choose step7.1 to run the bitcoin-cash server.  
Step 7.1  
```cd ~/bitcoin-cash-node```   
```pm2 start bitcore -- start```  

//if you didin't install pm2,please choose step7.2 to run the bitcoin-cash server.   
Step7.2  
```cd ~/bitcoin-cash-node```  
```bitcore start```

//////Done!!!!///////

**Check Something**

bitcoin-cash-node/package.json
```
{
  "description": "A full Bitcoin node build with Bitcore",
  "repository": "https://github.com/user/project",
  "license": "MIT",
  "readme": "README.md",
  "dependencies": {
    "bitcore-lib-cash": "^0.18.1",
    "bitcore-node": "^3.1.3",
    "insight-api": "^0.4.3",
    "insight-ui": "^0.4.0"
  }
}
```
[somewhere you want to sync and store the data]/bitcoin.conf
```
server=1
whitelist=127.0.0.1
txindex=1
addressindex=1
timestampindex=1
spentindex=1
zmqpubrawtx=tcp://127.0.0.1:28332
zmqpubhashblock=tcp://127.0.0.1:28332
rpcallowip=127.0.0.1
rpcuser=bitcoin
rpcpassword=local321
uacomment=bitcore
```
