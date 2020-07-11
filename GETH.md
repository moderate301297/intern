# GO ETHEREUM

## Giới thiệu

**GETH** là ethereum client giúp chúng ta có thể giao tiếp với mạng ETH blockchain, thực hiện các giao dịch, smart contract, mining.

**Keyconcept :**

**datadir :** thư mục lưu dữ liệu (key, log,..)

**port :**

**rpcport :** định nghĩa cổng rpc

**bootnode :** Giúp các node tìm thấy nhau trong mạng p2p, giống gateway giữa các node geth-miner với geth-tx, geth-tx public

### Cài đặt

**Ubuntu:**

> Run terminal:

```
sudo apt-get install software-properties-common
sudo add-apt-repository -y ppa:ethereum/ethereum
sudo apt-get update
sudo apt-get install ethereum
```

> Check version:

```
geth version
```

### Cấu trúc thư mục

**GETH** có thư mục mặc định tại:

```
~/.ethereum
```

- Có thể tạo thư mục mới theo tùy chọn người dùng

### Cấu hình và cài đặt file genesis 

> Tạo file genesis.json

```
{
    "config": {
        "chainId": 22,
        "homesteadBlock": 0,
        "eip155Block": 0,
        "eip158Block": 0
    },
    "difficulty": "0x400",
    "gasLimit": "0x2100000",
    "alloc": {
        "646cb67fa5f121e4ed674d9dbef8f1b177f20c3f": 
         { "balance": "0x1337000000000000000000" }     
    }
}
```

Cụ thể từng mục config như sau:

- **chainId**: id của blockchain của chúng ta. Ethereum không chỉ bao gồm 1 hệ thống blockchain duy nhất mà thực tế là có rất nhiều các network khác nhau. Hệ thống blockchain đang chạy thực tế có tên là `Mainnet` (chainid là 1), các network khác dành cho các mạng test trước khi lên production hoặc các mạng dành cho các phiên bản khác nhau của ethereum sẽ có các chainid khác, ví dụ: morden /expanse mainnet (2), ropsten (3), rinkeby (4), rootstock mainnet (30), rootstock testnet (31), kovan (42), ethereum classic mainnet (61), ethereum classic testnet (62). Private chain mặc định sẽ có id là `1337` theo khuyến cáo của [EIP 155](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-155.md).
- **homesteadBlock**: bằng 0 nghĩa là chúng ta đang sử dụng phiên bản `homestead` của ethereum. Gần đây thì Ethereum đã nâng câp lên phiên bản `byzantium` vào ngày 16/10/2017.
- **eip155Block**: bằng 0 nghĩa là chain chúng ta sẽ hỗ trợ EIP 155, tập hợp các định nghĩa giao thức, client API, các tiêu chuẩn dành cho smart contract.
- **eip158Block**: tương tự như trên
- **difficulty**: độ khó của chain, giá trị này sẽ ảnh hưởng đến *block time*, khoảng thời gian trung bình cần thiết để một block mới được sinh ra. Chú ý là một khi đã chạy blockchain rồi thì sẽ không thay đổi được giá trị này nữa. Trong ví dụ của chúng ta thì độ khó được thiết lập rất dễ nên với 1 máy tính cấu hình bình thường và 1 thợ mỏ duy nhất là đủ để vận hành cả hệ thống rồi.
- **gasLimit**: gas là giá nội bộ dùng để chạy các giao dịch hoặc hợp đồng trên Ethereum. Mỗi lệnh tính toán sẽ được gửi đến EVM (Ethereum Virtual Machine) và để chạy 1 lệnh cụ thể sẽ tiêu tốn một số lượng gas tương ứng. Nếu số gas mà người thực hiện không cung cấp đủ thì khi chạy đến giữa chừng, hợp đồng/giao dịch đó sẽ bị thất bại và số gas đã tiêu tốn sẽ bị lãng phí. Khi thực hiện giao dịch, bạn sẽ chỉ định *gasLimit*. Số gas tối đa mà bạn muốn trả để thực hiện giao dịch đó. Còn ở đây, ta chỉ định tổng số *gasLimit* của tất cả giao dịch ở trong block.
- **alloc**: Thiết lập này cho phép nạp sẵn Ether cho một số tài khoản định trước.

> Run file config:

```
geth --datadir path_data init path/genesis.json
```

Chúng ta có thể cấu hình file genesis thông qua _puppeth_:

>  Install puppeth: 

```
sudo apt install puppeth
```

> Run puppeth:

```
puppeth
```

### Chạy bootnode

> Thiết lập cho giao tiếp giữa các Node

> > Generate a key and start the boot node on any random port:

```
bootnode -genkey boot.key
bootnode -nodekey -addr :8009
```

### Chạy miner

> 

```
geth --datadir path/bootnode --nodiscover --syncmode ‘full’ -verbosity 6 --ipcdisable --port 30303 --bootnodes ‘enode://75e8bb7681194be0c77273454a03c328921efe81b6523f8c1e5eb819e9ad8ba676ed099b279484a8884f29cc7d5f63b5ad9d8ca655a62b3c7fc74b8f56295a2e@127.0.0.1:0?discport=8009’ --networkid 9876 --gasprice ‘1’ -unlock ‘0x219789a1844eF774Da4810e0437A105989b76332’ --password password.txt --mine
```

### Chạy peer nodes

> Peer nodes are started with the details of
>
> 1. Data directory
> 2. RPC ports to use
> 3. Network id (in genesis file)
> 4. Bootnode to use
> 5. APIs that are available on the node

```
geth --datadir path/node --nodiscover --syncmode ‘full’ -verbosity 6 --ipcdisable --port 30301 --rpc --rpcaddr ‘localhost’ --rpcport 8101 --rpcapi admin,debug,eth,miner,net,personal,shh,txpool,web3 --bootnodes ‘enode://75e8bb7681194be0c77273454a03c328921efe81b6523f8c1e5eb819e9ad8ba676ed099b279484a8884f29cc7d5f63b5ad9d8ca655a62b3c7fc74b8f56295a2e@127.0.0.1:0?discport=8009’ --networkid 9876
```

### **Attaching to peer nodes**

> Connect to a node

```
geth attach http://localhost:8101
```