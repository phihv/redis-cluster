# REDIS CLUSTER
## I. Các thao tác cơ bản
### 1. Kiểm tra kết nối cluster
```
 docker exec -it redis1 redis-cli cluster info
```

```
cluster_state:ok
cluster_slots_assigned:16384
cluster_slots_ok:16384
cluster_slots_pfail:0
cluster_slots_fail:0
cluster_known_nodes:6
cluster_size:3
cluster_current_epoch:7
cluster_my_epoch:7
cluster_stats_messages_ping_sent:1042
cluster_stats_messages_pong_sent:1065
cluster_stats_messages_sent:2107
cluster_stats_messages_ping_received:1065
cluster_stats_messages_pong_received:1041
cluster_stats_messages_fail_received:2
cluster_stats_messages_update_received:6
cluster_stats_messages_received:2114
total_cluster_links_buffer_limit_exceeded:0
```
### 2. Kiểm tra các nodes
```
docker exec -it redis1 redis-cli cluster nodes
```

```
7e0089c57a7808b7ae7dcdac7a647a7fe53272ab 172.19.0.3:6379@16379 slave 92f0354c77cd955fc687a6a108946143aadfffdf 0 1735528738000 2 connected
92f0354c77cd955fc687a6a108946143aadfffdf 172.19.0.5:6379@16379 master - 0 1735528738000 2 connected 5461-10922
e06e7fc82910559404c30c92d8f7d3930cb18eba 172.19.0.4:6379@16379 master - 0 1735528736329 7 connected 0-5460
00a01b46447ec2cbda81380c0d83772c2ec3c0bd 172.19.0.7:6379@16379 myself,slave e06e7fc82910559404c30c92d8f7d3930cb18eba 0 0 7 connected
d9571b3add1191255f724108a9f9d254748d2d7d 172.19.0.6:6379@16379 master - 0 1735528739365 3 connected 10923-16383
fb46206e4148f16e8fff15c2053a9a56f0c9fe15 172.19.0.2:6379@16379 slave d9571b3add1191255f724108a9f9d254748d2d7d 0 1735528738353 3 connected
```

- Node ID: Là mã định danh duy nhất của node, ví dụ e06e7fc82910559404c30c92d8f7d3930cb18eba.
- Địa chỉ: Địa chỉ IP và port của node, ví dụ 172.19.0.4:6379.
- Vai trò: master hoặc slave, xác định vai trò của node trong cluster.
- Slots: Nếu node là master, phần này chỉ ra dải slot mà node quản lý (ví dụ 0-5460).