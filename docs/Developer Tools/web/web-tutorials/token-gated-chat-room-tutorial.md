---
title: Web SDK - Token Gated Chat Room Tutorial
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
In this tutorial we will use LiveLike's chat APIs to build Gated Chat Rooms experience

## The Idea

**Token Gated Chat Rooms**\
The idea is to allow access to chat room for only those users who have the NFT(token)s minted from some specific contract addresses. For this integrator would be required to connect the user's crypto wallet and fetch the NFTs present in their wallet (owned by them)

For adding token gates to a chat room, producers can go to our CMS. Documentation can be found [here](https://docs.livelike.com/docs/token-gating-chat) about the same 

We will build gated chat room experience by using `getChatRoom` method which will load chat room only if the chat room doesn't have any token gates present

Integrators can also add listener to **chatroom-updated** even to track the updates happening to chat room and hence can decide to open/close chat room based on their updated token gates

```html index.html
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01//EN">
<html>
<head>
  <link rel="stylesheet" href="./style.css">
  <title>Token Gated Chat Rooms</title>
</head>

<body>

  <input type="text" name="roomId" id="roomId" placeholder="Enter Room Id" />
  <button id="enterChatRoom">Enter Chat Room</button>
  <br />
  <button id="listenToChatRoom">Listen To Chat Room Updates</button>
  <button id="stopListeningToChatRoom">
    Stop Listening To Chat Room Updates
  </button>
  <div class="chat-container">
    <h3>Chat Container</h3>
    <livelike-chat></livelike-chat>
  </div>
  <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.6.0/jquery.min.js"></script>
  <script src="https://cdn.ethers.io/lib/ethers-5.2.umd.min.js"
        type="application/javascript"></script>
  <script src="https://unpkg.com/@livelike/engagementsdk/livelike.umd.js"></script>
  <script src="./nft.js"></script>
  <script src="./script.js"></script>
  <script>
    LiveLike.init({
      clientId: "xxxxxxxxxxx"
    });
  </script>
</body>
</html>
```
```javascript nft.js
const provider = new ethers.providers.Web3Provider(window.ethereum);
const etherScanAPIkey = 'xxxxxxxxxxxxxxxx';
let userWallet;

async function getTokenBalance(contractaddress) {
  let url = `https://api-ropsten.etherscan.io/api?module=account&action=tokenbalance&contractaddress=${contractaddress}&address=${userWallet}&tag=latest&apikey=${etherScanAPIkey}`;
  const data = await fetch(url).then((res) => res.json());
  console.log(data.result);
  let tokens = parseInt(data.result);
  return tokens;
}

async function connectToWallet() {
  // Prompt user for account connections
  await provider.send('eth_requestAccounts', []);
  const signer = provider.getSigner();
  userWallet = await signer.getAddress();
  console.log(userWallet);
  // getTokenBalance(userWallet);
}

connectToWallet();
```
```javascript script.js
const chat = document.querySelector('livelike-chat');
const fetchChatRoom = () => {
  const roomId = $('#roomId').val();
  LiveLike.getChatRoom({ roomId }).then((chatRoomPayload) => {
    console.log('chatroom fetched', chatRoomPayload.token_gates);
    if (
      !chatRoomPayload.token_gates ||
      chatRoomPayload.token_gates.length <= 0
    ) {
      chat.roomid = roomId;
    } else {
      getTokenBalance(chatRoomPayload.token_gates[0].contract_address).then(
        (tokens) => {
          if (tokens) {
            chat.roomid = roomId;
          } else {
            chat.roomid = null;
            alert('You cannot enter this room, this room is token gated');
          }
        }
      );
    }
  });
};

$('#enterChatRoom').click(fetchChatRoom);

const listenerFn = (data) => {
  console.log('chatroom-updated', data);
  const roomId = $('#roomId').val();
  const chatRoomPayload = data.message;
  if (!chatRoomPayload.token_gates || chatRoomPayload.token_gates.length <= 0) {
    alert('Chatroom can be entered');
    chat.roomid = roomId;
  } else {
    getTokenBalance(chatRoomPayload.token_gates[0].contract_address).then(
      (tokens) => {
        if (tokens) {
          alert('Chatroom can be entered');
          chat.roomid = roomId;
        } else {
          chat.roomid = null;
          alert('You cannot enter this room, this room is token gated');
        }
      }
    );
  }
};

$('#listenToChatRoom').click(function () {
  console.log('started listening to chatroom updates');
  const roomId = $('#roomId').val();
  LiveLike.addChatRoomEventListener(
    LiveLike.ChatRoomEvent.CHATROOM_UPDATED,
    listenerFn,
    { roomId: roomId }
  );
});

$('#stopListeningToChatRoom').click(function () {
  console.log('stopped listening to chatroom updates');
  const roomId = $('#roomId').val();
  LiveLike.removeChatRoomEventListener(
    LiveLike.ChatRoomEvent.CHATROOM_UPDATED,
    listenerFn,
    { roomId: roomId }
  );
});
```
```css style.css
body {
  font-family: sans-serif;
}
#roomId {
  padding: 5px;
  width: 50%;
  margin-bottom: 10px;
}
.chat-container {
  padding: 10px;
  background-color: grey;
  margin-top: 10px;
}
```
