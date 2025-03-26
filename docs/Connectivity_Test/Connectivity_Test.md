# Connectivity Test with OAI
to run round-test trip (rtt) with OAI, make sure to setup the environment by :
[OAI Environment Setup](https://github.com/bmw-ece-ntust/internship/blob/2025-TEEP-8-Gavin/docs/OAI_Setup/OAI_Setup.md)

after environment pre-requisites, configs, and initial setups are done : 
## Run OAI CN5G
```
cd ~/oai-cn5g
docker compose up -d
```

## Run OAI gNB with RFSimulator (on another terminal)
```
cd ~/openairinterface5g/cmake_targets/ran_build/build
sudo ./nr-softmodem -O ../../../targets/PROJECTS/GENERIC-NR-5GC/CONF/gnb.sa.band78.fr1.106PRB.usrpb210.conf --gNBs.[0].min_rxtxtime 6 --rfsim
```

## Run OAI nrUE with RFSimulator (on another terminal)
```
cd ~/openairinterface5g/cmake_targets/ran_build/build
sudo ./nr-uesoftmodem -r 106 --numerology 1 --band 78 -C 3619200000 --uicc0.imsi 001010000000001 --rfsim
```

note : if nr-uesoftmodem config is not found, go to the directory and create a new config with 
```
nano ~/nrue.uicc.conf
```
and modify and save it to :
```
uicc0 = {
  imsi = "001010000000001";
  key = "fec86ba6eb707ed08905757b1bb44b8f";
  opc = "C42449363BBAD02B66D16BC975D77CC1";
  dnn = "oai";
  nssai_sst = 1;
}
```

## End-to-end connectivity test
(on another terminal)
```
ping 192.168.70.135 -I oaitun_ue1
```
press Ctrl+C to terminate the pinging process to see details of the test
