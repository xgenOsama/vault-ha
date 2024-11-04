```
docker-compose up -d
docker exec -it vault1 vault operator init
# After running the initialization command, Vault will output:
# 1- Unseal Keys (multiple keys)
# 2- Root Token
# Step 2: Unseal vault1
docker exec -it <vault1-container-id> vault operator unseal <UNSEAL_KEY_1>
docker exec -it <vault1-container-id> vault operator unseal <UNSEAL_KEY_2>
docker exec -it <vault1-container-id> vault operator unseal <UNSEAL_KEY_3>
# step 3: Use the following command to have vault2 join the cluster
docker exec -it vault2 vault operator raft join http://vault1:8202
# Step 4: Unseal vault2
Since vault2 is now part of the cluster, it shares the same unseal keys as vault1. Follow the same steps to unseal vault2:
docker exec -it <vault2-container-id> vault operator unseal <UNSEAL_KEY_1>
docker exec -it <vault2-container-id> vault operator unseal <UNSEAL_KEY_2>
docker exec -it <vault2-container-id> vault operator unseal <UNSEAL_KEY_3>
# Step 5: Verify the Cluster
```# vault-ha
