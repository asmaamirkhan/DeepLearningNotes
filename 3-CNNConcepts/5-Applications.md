# Common Applications of CNNs

| Application       | Description   |
| ----------------- | ------------- |
| Face Verification | Recognizing if that the given image and ID are belonging to the same person |
| Face Recognition  | Assigning ID to the input face image |


## Face Verification
### Comparison

| Term              | Description                              | Input           | Output       | Problem Class |
| ----------------- | ---------------------------------------- | --------------- | ------------ | ------------- |
| Face Verification | Cheking that this is the wanted person   | Face image / ID | True / False | 1:1           |
| Face Recognition  | Assigning ID to the input face image     | Face image      | ID of `K` faces in DB | 1:K  |

### Solving Approach

#### 🤳 One Shot Learning
Learning form one example (that we have in the database) to recognize the person again 

#### The Process
- Get input image
- Check if it bilongs to the faces you have in the DB
- 

#### How to Check? 👓

We have to calculate the _similarity_ between the input image and the image in the database, so:

- Use some function that 
  - similarity(img_in, img_db) = some_val
- Specifiy a threshold value
- Check the threshold and specify the output

#### What can the similarity function can be? 👀

Siamese Network:

> TODO