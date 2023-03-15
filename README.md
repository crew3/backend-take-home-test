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
## Expected output
```jsonc
{
  "status": "success" // can be fail or success,
  "score": 3, // integer between 0 and 10
}
```
For a quest to be considered successful, the following criteria must be met:
- It satisfies all access conditions (NFT, date and level). Keep in mind that not all access conditions might be there.
- The quest has not been previously completed by the user.
- The score is greater or equal than 5.

## Score algorithm
The score should be computed using the submission_text string:
- Initialize a score variable to 0.
- Check if the input string is empty. If it is, return a score of 0.
- Check if the input string contains only whitespace characters. If it does, return a score of 1.
- Check if the input string contains only digits. If it does, return a score of 2.
- Check if the input string contains only uppercase letters. If it does, return a score of 3.
- Check if the input string contains only lowercase letters. If it does, return a score of 4.
- Check if the input string contains both uppercase and lowercase letters. If it does, return a score of 5.
- Check if the input string contains at least one punctuation character (",", ".", "?", "!"). If it does, return a score of 6.
- Check if the input string contains at least one special character (@, #, $, %, ^, &, *). If it does, return a score of 7.
- Check if the input string is a palindrome. If it is, return a score of 8.
- Check if the input string contains any repetitive sequences (such as "aaa" or "abaaba"). If it does, return a score of 9.
If none of the above conditions apply, return a score of 10.

## Bonus
On the score computation, check if the input string contains any offensive language or hate speech. If it does, return a score of 0.

