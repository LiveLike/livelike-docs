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
[block:api-header]
{
  "title": "The Idea"
}
[/block]
**Token Gated Chat Rooms** 
The idea is to allow access to chat room for only those users who have the NFT(token)s minted from some specific contract addresses. For this integrator would be required to connect the user's crypto wallet and fetch the NFTs present in their wallet (owned by them)

For adding token gates to a chat room, producers can go to our CMS. Documentation can be found [here](https://docs.livelike.com/docs/token-gating-chat) about the same 

We will build gated chat room experience by using `getChatRoom` method which will load chat room only if the chat room doesn't have any token gates present

Integrators can also add listener to **chatroom-updated** even to track the updates happening to chat room and hence can decide to open/close chat room based on their updated token gates
[block:code]
{
  "codes": [
    {
      "code": "<!DOCTYPE html PUBLIC \"-//W3C//DTD HTML 4.01//EN\">\n<html>\n<head>\n  <link rel=\"stylesheet\" href=\"./style.css\">\n  <title>Token Gated Chat Rooms</title>\n</head>\n\n<body>\n\n  <input type=\"text\" name=\"roomId\" id=\"roomId\" placeholder=\"Enter Room Id\" />\n  <button id=\"enterChatRoom\">Enter Chat Room</button>\n  <br />\n  <button id=\"listenToChatRoom\">Listen To Chat Room Updates</button>\n  <button id=\"stopListeningToChatRoom\">\n    Stop Listening To Chat Room Updates\n  </button>\n  <div class=\"chat-container\">\n    <h3>Chat Container</h3>\n    <livelike-chat></livelike-chat>\n  </div>\n  <script src=\"https://ajax.googleapis.com/ajax/libs/jquery/3.6.0/jquery.min.js\"></script>\n  <script src=\"https://cdn.ethers.io/lib/ethers-5.2.umd.min.js\"\n        type=\"application/javascript\"></script>\n  <script src=\"https://unpkg.com/@livelike/engagementsdk/livelike.umd.js\"></script>\n  <script src=\"./nft.js\"></script>\n  <script src=\"./script.js\"></script>\n  <script>\n    LiveLike.init({\n      clientId: \"xxxxxxxxxxx\"\n    });\n  </script>\n</body>\n</html>",
      "language": "html",
      "name": "index.html"
    },
    {
      "code": "const provider = new ethers.providers.Web3Provider(window.ethereum);\nconst etherScanAPIkey = 'xxxxxxxxxxxxxxxx';\nlet userWallet;\n\nasync function getTokenBalance(contractaddress) {\n  let url = `https://api-ropsten.etherscan.io/api?module=account&action=tokenbalance&contractaddress=${contractaddress}&address=${userWallet}&tag=latest&apikey=${etherScanAPIkey}`;\n  const data = await fetch(url).then((res) => res.json());\n  console.log(data.result);\n  let tokens = parseInt(data.result);\n  return tokens;\n}\n\nasync function connectToWallet() {\n  // Prompt user for account connections\n  await provider.send('eth_requestAccounts', []);\n  const signer = provider.getSigner();\n  userWallet = await signer.getAddress();\n  console.log(userWallet);\n  // getTokenBalance(userWallet);\n}\n\nconnectToWallet();\n",
      "language": "javascript",
      "name": "nft.js"
    },
    {
      "code": "const chat = document.querySelector('livelike-chat');\nconst fetchChatRoom = () => {\n  const roomId = $('#roomId').val();\n  LiveLike.getChatRoom({ roomId }).then((chatRoomPayload) => {\n    console.log('chatroom fetched', chatRoomPayload.token_gates);\n    if (\n      !chatRoomPayload.token_gates ||\n      chatRoomPayload.token_gates.length <= 0\n    ) {\n      chat.roomid = roomId;\n    } else {\n      getTokenBalance(chatRoomPayload.token_gates[0].contract_address).then(\n        (tokens) => {\n          if (tokens) {\n            chat.roomid = roomId;\n          } else {\n            chat.roomid = null;\n            alert('You cannot enter this room, this room is token gated');\n          }\n        }\n      );\n    }\n  });\n};\n\n$('#enterChatRoom').click(fetchChatRoom);\n\nconst listenerFn = (data) => {\n  console.log('chatroom-updated', data);\n  const roomId = $('#roomId').val();\n  const chatRoomPayload = data.message;\n  if (!chatRoomPayload.token_gates || chatRoomPayload.token_gates.length <= 0) {\n    alert('Chatroom can be entered');\n    chat.roomid = roomId;\n  } else {\n    getTokenBalance(chatRoomPayload.token_gates[0].contract_address).then(\n      (tokens) => {\n        if (tokens) {\n          alert('Chatroom can be entered');\n          chat.roomid = roomId;\n        } else {\n          chat.roomid = null;\n          alert('You cannot enter this room, this room is token gated');\n        }\n      }\n    );\n  }\n};\n\n$('#listenToChatRoom').click(function () {\n  console.log('started listening to chatroom updates');\n  const roomId = $('#roomId').val();\n  LiveLike.addChatRoomEventListener(\n    LiveLike.ChatRoomEvent.CHATROOM_UPDATED,\n    listenerFn,\n    { roomId: roomId }\n  );\n});\n\n$('#stopListeningToChatRoom').click(function () {\n  console.log('stopped listening to chatroom updates');\n  const roomId = $('#roomId').val();\n  LiveLike.removeChatRoomEventListener(\n    LiveLike.ChatRoomEvent.CHATROOM_UPDATED,\n    listenerFn,\n    { roomId: roomId }\n  );\n});\n",
      "language": "javascript",
      "name": "script.js"
    },
    {
      "code": "body {\n  font-family: sans-serif;\n}\n#roomId {\n  padding: 5px;\n  width: 50%;\n  margin-bottom: 10px;\n}\n.chat-container {\n  padding: 10px;\n  background-color: grey;\n  margin-top: 10px;\n}\n",
      "language": "css",
      "name": "style.css"
    }
  ]
}
[/block]