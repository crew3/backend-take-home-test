# Quester - Backend Take Home Assignment

Crew3 functions as a central hub for web3 communities, where contributors gather to learn, engage, and discover new communities. The bedrock of the engagement mechanism lies in its quests, which are are designed to be modulable, fun and intuitive.

For this assignement, you will create a simple version of our claim quest endpoint. Given a JSON payload that represents a quess submission, the endpoint should return a JSON response that includes the submission's success status and a score that reflects the submission's quality. 

## The input
```jsonc
{
  "questId": "4569bee2-8f42-4054-b432-68f6ddbc20b5", // uuid
  "userId": "cb413e98-44a4-4bb1-aaa1-0b91ab1707e7", // uuid
  "claimed_at": "2023-03-15T10:44:22+0000", // date in ISO 8601 format
  "access_condition": [ // array of condition object, variable in size
   {
      "type": "nft", //check if a user NFTs contain/notContain a specific ID
      "operator": "contains", //can be "contains" or "notContains"
      "value": "0x1" // Id of the NFT
   },
   {
     "type": "date", // check if the claimed_at date is > or < to the specified value
     "value": "2023-02-15T10:44:22+0000",
     "operator": ">" //can be ">" or "<"
   },
   {
     "type": "level", // check if the user level is > or < to the specified value
     "value": "4", // positive integer
     "operator": ">" // operator can be ">" or "<"
   }
  ],
  "user_data": {
    "completed_quests": [
      "94e2e33e-07e9-4750-8cea-c033d7706057"
    ], // array of uuid
    "nfts": ["Ox1", "0x2"], // array of NFTs ID (hexadecimal)
    "level": 3 // positive integer
  },
  "submission_text": "Lorem ipsum dolor sit amet.", // string
}
```
## Algorithm
