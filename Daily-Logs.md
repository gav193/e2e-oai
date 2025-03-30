# Daily Logs
## 2025/03/22
**Short-term Goals**
1. Install OAI and do end-to-end test (rtt or round-test trip)
   - [Install VM with Virtual Box](https://www.virtualbox.org/wiki/Downloads)
   - [Install Ubuntu ISO and set-up VM for Ubuntu](https://ubuntu.com/download/desktop)
   - [Install OAI and testing environment](https://gitlab.eurecom.fr/oai/openairinterface5g)
2. Create documentation of the process
3. Draft IEEE document of the test

**Daily Logs**:
- 21.30-22.00 : [Install Virtual Box](https://github.com/bmw-ece-ntust/internship/blob/2025-TEEP-8-Gavin/docs/Virtual_Box_Installation.png)
- 22.00-22.30 : [Install Ubuntu and create a VM](https://github.com/bmw-ece-ntust/internship/blob/2025-TEEP-8-Gavin/docs/Ubuntu_Setup.png)

## 2025/03/23
**Short-term Goals**
1. Install OAI and do end-to-end test (rtt or round-test trip)
   - [Install VM with Virtual Box](https://www.virtualbox.org/wiki/Downloads)
   - [Install Ubuntu ISO and set-up VM for Ubuntu](https://ubuntu.com/download/desktop)
   - [Install OAI and testing environment](https://gitlab.eurecom.fr/oai/openairinterface5g)
2. Create documentation of the process
3. Draft IEEE document of the test

**Daily Logs**:
- 21.00-22.00 : [Reinstall Ubuntu due to outdated version](https://github.com/bmw-ece-ntust/internship/blob/2025-TEEP-8-Gavin/docs/Ubuntu_Setup.png)

## 2025/03/24
**Short-term Goals**
1. Install OAI and do end-to-end test (rtt or round-test trip)
   - [Install VM with Virtual Box](https://www.virtualbox.org/wiki/Downloads)
   - [Install Ubuntu ISO and set-up VM for Ubuntu](https://ubuntu.com/download/desktop)
   - [Install OAI and testing environment](https://gitlab.eurecom.fr/oai/openairinterface5g)
2. Create documentation of the process
3. Draft IEEE document of the test

**Daily Logs**:
- 08.00-10.00 : [Set up ISO file and VM for Ubuntu](https://github.com/bmw-ece-ntust/internship/blob/2025-TEEP-8-Gavin/docs/Ubuntu_Setup.png)
- 10.01-12.00 : [Read through documentation of OAI online](https://gitlab.eurecom.fr/oai/openairinterface5g)

## 2025/03/25
**Short-term Goals**
1. Install OAI and do end-to-end test (rtt or round-test trip)
   - [Set up OAI CN5G, gNB, and UE](https://gitlab.eurecom.fr/oai/openairinterface5g)
   - [Test end-to-end connectivity](https://gitlab.eurecom.fr/oai/openairinterface5g/-/blob/develop/doc/README.md#tutorials)
2. Create documentation of the process
3. Draft IEEE document of the test

**Daily Logs**:
- 11.00-11.30 : Set up CN5G pre-requisites, configurations, and docker images
   - [Set up CN5G docker](https://github.com/bmw-ece-ntust/internship/blob/2025-TEEP-8-Gavin/docs/OAI_Setup/CN-5G_docker_pull.png)
   - [Test run and start CN5G](https://github.com/bmw-ece-ntust/internship/blob/2025-TEEP-8-Gavin/docs/OAI_Setup/CN-5G_startup.png)
- 11.31-12.30 : Build UHD and OAI gNB
   - [Build UHD from source and test](https://github.com/bmw-ece-ntust/internship/blob/2025-TEEP-8-Gavin/docs/OAI_Setup/UHD_Build_test.png)
   - [Build and test run gNB](https://github.com/bmw-ece-ntust/internship/blob/2025-TEEP-8-Gavin/docs/OAI_Setup/gNB_test_run.png)
- 13.00-13.30 : [Error due to no USRP device found](https://github.com/bmw-ece-ntust/internship/blob/2025-TEEP-8-Gavin/docs/OAI_Setup/gNB_run_error.png)
- 13.31-14.00 : [Ran RFSimulator for gNB](https://github.com/bmw-ece-ntust/internship/blob/2025-TEEP-8-Gavin/docs/OAI_Setup/gNB_run_RFSim.png)
- 14.01-15.30 : [Tried running OAI UE with RFSimulator](https://github.com/bmw-ece-ntust/internship/blob/2025-TEEP-8-Gavin/docs/OAI_Setup/gNB_with_UE_initial_run.png)
   - Initially found error from unspecified directory "./nr-uesoftmodem"
   - [Fixed error by renewing config file nrUE](https://github.com/bmw-ece-ntust/internship/blob/2025-TEEP-8-Gavin/docs/OAI_Setup/nrue_config.png)
- 15.31-16.30 : [Ran OAI UE with RFSimulator](https://github.com/bmw-ece-ntust/internship/blob/2025-TEEP-8-Gavin/docs/Connectivity_Test/UE_problem.png)
   - gNB doesn't respond to UE updates and pings -> UE connectivity problem
   - [Connectivity check from system ports](https://github.com/bmw-ece-ntust/internship/blob/2025-TEEP-8-Gavin/docs/Connectivity_Test/IP_routing_check.png) -> found that the target port is not connected to system, hinting at UE to gNB disconnection
   - [IP routing check](https://github.com/bmw-ece-ntust/internship/blob/2025-TEEP-8-Gavin/docs/Connectivity_Test/further_IP_routing_check.png) -> found oaitun_ue1 but connected at wrong address, hinting at UE startup mismatch or wrong routing within local system which is also proven through very small rtt values on initial test
   - [oaitun_ue1 connectivity check](https://github.com/bmw-ece-ntust/internship/blob/2025-TEEP-8-Gavin/docs/Connectivity_Test/oaitun_ue1_routing.png) -> same conclusion from previous ip check, hinting a high possibility of UE routing problem
- 16.31-17.00 : Fixed ping error by opening up new terminal for UE, ran end-to-end connectivity test
   - [Restarted gNB](https://github.com/bmw-ece-ntust/internship/blob/2025-TEEP-8-Gavin/docs/Connectivity_Test/UE_run_solved.png)
   - [Restarted UE](https://github.com/bmw-ece-ntust/internship/blob/2025-TEEP-8-Gavin/docs/Connectivity_Test/gNB_run_solved.png)
   - [Opened a new terminal specifically for ping test]([https://github.com/bmw-ece-ntust/internship/blob/2025-TEEP-8-Gavin/docs/Connectivity_Test/connectivity_rtt.png](https://github.com/bmw-ece-ntust/internship/blob/2025-TEEP-8-Gavin/docs/Connectivity_Test/Connectivity_RTT.png)) -> ping successful marking that RTT is successful and connection between UE and gNB is established

## 2025/03/26
**Short-term Goals**
1. Install OAI and do end-to-end test 
2. Create documentation of the process (in progress)
3. Draft IEEE document of the test (in progress)

**Daily Logs**:
- 11.00-11.30 : Drafted outline for IEEE paper
- 13.00-16.00 : Filtering references online for IEEE paper

## 2025/03/27
**Short-term Goals**
1. Install OAI and do end-to-end test 
2. Create documentation of the process (in progress)
3. Draft IEEE document of the test (in progress)

**Daily Logs**:
- 13.00-17.00 : Worked on IEEE paper analysis and several other parts of the paper

## 2025/03/28
**Short-term Goals**
1. Install OAI and do end-to-end test 
2. Create documentation of the process (in progress)
3. Draft IEEE document of the test (in progress)

**Daily Logs**:
- 13.00-15.00 : Researched online references and fixed formatting issues on IEEE paper
- 15.01-17.00 : Finished initial rough draft of IEEE paper

## 2025/03/29
**Short-term Goals**
1. Install OAI and do end-to-end test 
2. Create documentation of the process (in progress)
3. Draft IEEE document of the test (in progress)

**Daily Logs**:
- 13.00-15.00 : Finished IEEE paper documentation

## 2025/03/30
**Short-term Goals**
1. Install OAI and do end-to-end test 
2. Create documentation of the process (in progress)
3. Draft IEEE document of the test 

**Daily Logs**:
- 15.00-17.00 : Preparing to uplaod IEEE document on GitHub for documentation

## 2025/03/30
**Short-term Goals**
1. Install OAI and do end-to-end test 
2. Create documentation of the process
3. Draft IEEE document of the test 

**Daily Logs**:
- 04.00-04.10 : Uploaded IEEE document on GitHub
