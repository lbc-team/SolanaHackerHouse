
## solana

### 安装 Rust 和 Solana CLI

```shell
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh

sh -c "$(curl -sSfL https://release.solana.com/v1.16.14/install)"
```

查看版本

```shell
rustc -V

solana -V
```

更多内容请查看：

https://www.rust-lang.org/tools/install

https://docs.solana.com/cli/install-solana-cli-tools

### solana 常用命令

#### acount

```shell
solana-keygen new -o ./solana/id.json # 生成地址

solana address # 查看地址

solana balance # 查询余额

solana airdrop 1 # 水龙头
```

#### 配置

```shell
solana config set --url localhost # 设定 rpc 为本地环境
solana config set --url devnet # 设定 rpc 为开发环境

solana config get # 获取配置信息
```

#### 运行本地测试节点

```shell
solana-test-validator
```

#### 通过水龙头 获取测试币

```shell
solana airdrop 1 #每次不要请求太多 coin，时间不要太频繁
```

#### 转账

```shell
solana transfer <address>  1
solana transfer --allow-unfunded-recipient <address> 1
```

#### 部署合约

```shell
solana program deploy <path>

# 编译好的合约文件是个so文件，路径是 "./target/deploy/hello.so"
```

#### 查看合约日志（只能在本地网络生效）

```shell
solana logs <PROGRAM_ID>

solana logs DKtPpFnJoMn6qUFiPxWN61DJqFqPpYoGShrwaG2QJfRx
```

### 释放合约

部署合约非常消耗 SOL，这些 SOL 作为合约的存储费用。
如果合约不再使用，可以用命令释放掉合约，可以指定接收地址，支付的 SOL 就会返还。

```shell
solana program close
# .....

solana program close  --buffers

Buffer Address                               | Authority                                    | Balance
ER5KN9u6uy9N8d2TPFLwUhuBXwmbz5TDYZuR9tiXctTu | HxJHFKt8nFxmXL8HVnD84YJFrsZmHC1ux9fgwm2awkS8 | 3.42752856 SOL
HczChndCYcydwemUsNqePGZzE139NnoVbnWZ6d8PQudE | HxJHFKt8nFxmXL8HVnD84YJFrsZmHC1ux9fgwm2awkS8 | 0.2798268 SOL
9PWdoUoZ2q76x7dZCWUqoabnpmGdEAh5xp5ub1bV9Pz5 | HxJHFKt8nFxmXL8HVnD84YJFrsZmHC1ux9fgwm2awkS8 | 0.2798268 SOL
8q9B696b3ZWVNTuikNsrwBfXRnew3hcqoKiBGzeD4uz9 | HxJHFKt8nFxmXL8HVnD84YJFrsZmHC1ux9fgwm2awkS8 | 0.2798268 SOL
```

## Solana 地址

Solana 上有三种类型的账户：

- 数据帐户 - 就是用来存储数据的
- 程序帐户 - 存储可执行程序（又称智能合约）的地方
- 原生账户 - 用于核心区块链功能，例如权益和投票的账户

### 原生账户

原生账户是个固定的地址，地址是 `11111111111111111111111111111111`。

```js
export class SystemProgram {

  static programId: PublicKey = new PublicKey(
    '11111111111111111111111111111111',
  );
}
```

更多内容请看：https://solana-labs.github.io/solana-web3.js/classes/SystemProgram.html

### PDA 地址

PDA = Program Derived Addresses，程序派生地址。

PDA 是一种特殊类型的账户，它们只是一种特殊的地址，不是真正的账户。它们由程序控制，而不是私钥。因为 PDA 没有私钥，因此无法对其进行签名。

![](./pda.jpg)

普通的 Solana 账户是由 [Ed25519](https://ed25519.cr.yp.to/) 签名系统创建的，而 PDA 由程序控制。因此，我们使用不在 Ed25519 曲线上的地址来制作 PDA。

Polkadot 也使用了 Ed25519 算法生成地址。

![](./ed25519.jpg)

它提供了链上和链下程序确定性地定位数据的方法。可以将其视为一个键值存储，其中 seeds、programId 和 bump 结合形成密钥，以及网络在该地址上存储的值。

**每个账户有 10 Mb 的限制。**

#### findProgramAddressSync

我们可以通过 `findProgramAddressSync` 查找 PDA。

```js
static findProgramAddressSync(
  seeds: Array<Buffer | Uint8Array>,
  programId: PublicKey,
): [PublicKey, number] {
  let nonce = 255;
  let address;
  while (nonce != 0) {
    try {
      const seedsWithNonce = seeds.concat(Buffer.from([nonce]));
      address = this.createProgramAddressSync(seedsWithNonce, programId);
    } catch (err) {
      if (err instanceof TypeError) {
        throw err;
      }
      nonce--;
      continue;
    }
    return [address, nonce];
  }
  throw new Error(`Unable to find a viable program address nonce`);
}
```

更多内容请看：https://solana-labs.github.io/solana-web3.js/classes/PublicKey.html#findProgramAddressSync

## 工具

https://sol-tools.tonyboyle.io/nft-tools

https://github.com/cryptoloutre/solana-tools

## 钱包

- Phantom https://phantom.app/
- Glow https://glow.app/
- BackPack https://www.backpack.app/ 需要登录

## SPL
https://spl-token-faucet.com/

## NFT

https://www.metaplex.com/ 类似 erc721

## NFT explorer

https://app.step.finance/

https://solana.nftscan.com/ 只支持主网

https://magiceden.io/ 支持 solana、eth、polygon

---

参考：

https://docs.solana.com/api/http

https://www.datawallet.com/crypto/how-to-get-solana-faucet-tokens
