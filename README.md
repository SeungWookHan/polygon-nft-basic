## Mint NFTs on Polygon testnets

> [원본 링크](https://wiki.polygon.technology/docs/develop/nftstorage/)

### Introduction

해당 튜토리얼에서는 NFT.storage, Polygon 뭄바이 테스트넷 계정, Hardhat을 이용해 샘플 이미지를  
NFT, 즉 대체 불가능한 토큰으로 배포하는 것을 진행합니다.  
폴더의 구조는 크게 3가지 입니다.

> assets: 이미지 등 NFT화 할 데이터를 넣는 곳  
> scripts: 이미지를 metadata화, 컨트랙트 배포, NFT 민팅에 대한 스크립트 모음  
> contracts: ERC-721 컨트랙트

사전에 Metamask 또는 기타 지갑을 활용해 Polygon 계정을 만들고, 테스트 Matic을 받았고, NFT.storage에 회원가입하여 API키를 받았다는 가정하로 진행합니다.

> 자세한 사항은 원본 링크를 확인해주세요.

### Instruction

1. Node.js 종속성 설치

```
npm install
```

2. .env 작성

```
mv .env.example .env
```

```
PRIVATE_KEY="폴리곤 계정의 프라이빗 키"
NFT_STORAGE_API_KEY="NFT.storage API 키"
```

3. assets에 민팅하고자 하는 이미지 넣기

4. store-asset.mjs 실행
   > 이때 해당 파일의 name, description, image의 경로를 적절하게 수정합니다.

```
node scripts/store-asset.mjs
```

실행 후 아래와 같은 ipfs:// 시작하는 URL이 나오면 따로 저장해두거나 기억해둡니다.

```
Metadata stored on Filecoin and IPFS with URL:  ipfs://HASH/metadata.json

```

5. deploy-contract.mjs 실행

```
npx hardhat run scripts/deploy-contract.mjs --network PolygonMumbai

```

명령어 실행 후 아래와 같은 0x로 시작하는 address가 나오면 따로 저장해두거나 기억해둡니다.

```
Contract deployed to address: 0x{컨트랙트 주소}
```

6. mint-nft.mjs 실행
   > 이때 해당 파일의 CONTRACT_ADDRESS, META_DATA_URL의 값을 각각 5번에서 구한 값, 4번에서 구한 값으로 적절하게 수정합니다.

```
npx hardhat run scripts/mint-nft.mjs \--network PolygonMumbai
```

명령어 실행 후 아래와 같이 내 주소로 성공적으로 민팅이 되었다는 문구가 나오면 성공입니다.

```
NFT minted to:  0x{폴리곤 주소}
```
