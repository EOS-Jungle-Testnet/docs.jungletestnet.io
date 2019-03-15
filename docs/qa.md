---
id: qa
title: Questions & Answers
sidebar_label: Questions & Answers
---

## Q&A


1. How init node first time 
	- Run ./start.sh --delete-all-blocks --genesis-json genesis.json in **\<NODE\>** folder

2. Create EOSIO account
	- ./cleos.sh system newaccount --stake-net "10.0000 EOS" --stake-cpu "10.0000 EOS" --buy-ram-kbytes 4 **\<your accountr\>** **\<new account\>** **\<owner_pup_key\>** **\<active_pub_key\>**

3. Send EOS
	- ./cleos.sh transfer **\<your account\>**  **\<receiver account\>** "1.0000 EOS" "test memo text"

4. Get Balance
	- ./cleos.sh get currency balance eosio.token **\<account name\>**

5. List registered producers (-l **\<limit\>**)
	- ./cleos.sh get table eosio eosio producers -l 100

6. List staked/delegate
	- ./cleos.sh system listbw **\<account\>**

7. how can I check  REX balance
	- ./cleos.sh get table eosio eosio rexbal
	- ./cleos.sh get table eosio eosio rexpool
	- ./cleos.sh get table eosio eosio rexfund
	- ./cleos.sh get table eosio eosio cpuloan
	- ./cleos.sh get table eosio eosio netloan
	- ./cleos.sh get table eosio eosio delband
	- ./cleos.sh get table eosio eosio rexqueue

8. Deposit:
	- ./cleos.sh push action eosio deposit '{"owner":"**\<YOUR ACC\>**","amount":"**\<AMOUNT\>** EOS"}' -p **\<YOUR ACC\>**

9. Rent CPU
	- ./cleos.sh push action eosio rentcpu '{"from":"**\<YOUR ACC\>**","receiver":"**\<YOUR OR SOMEOENE ACC\>**","loan_payment":"**\<AMOUNT\>** EOS","loan_fund":"**\<AMOUNT\>** EOS"}' -p **\<YOUR ACC\>**

10. Buy REX
	- ./cleos.sh push action eosio buyrex '{"from":"**\<YOUR ACC\>**","amount":"**\<AMOUNT\>** EOS"}' -p **\<YOUR ACC\>**

11. Snapshot(only for Ubuntu16/18) for oldschool full backup
	- [Ubuntu18](http://backup.jungletestnet.io/ubuntu18/)
	- [Ubuntu16](http://backup.jungletestnet.io/ubuntu16/)
	- restore: download last block and state for your OS, extract their and replace in your **\<NODE\>** folder
12. Oldschool full backup
	- stop node
	- copy blocks and state folder(if you have the backup or download it from http://backup.jungletestnet.io (ubuntu 16/18)) 
	- start node

13. Snapshot system in 1.4 (described here https://github.com/EOSIO/eos/pull/5956) very fast but no access to old blocks after recover, plugin **\<producer_api_plugin\>** must be enabled
	- create: curl -sS http://127.0.0.1:8888/v1/producer/create_snapshot | jq '.'
		```
		{
		  "head_block_id": "0077d693b072b92aec7d1af86f753995ff7daeeb2316616f9e3e341e44689836",
		  "snapshot_name": "<data-dir>/snapshots/snapshot-0077d693b072b92aec7d1af86f753995ff7daeeb2316616f9e3e341e44689836.bin"
		}
		```
	- restore: ./start --snapshot **\<path to snapshot\>**
