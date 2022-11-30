# video_to_mp3_microservices


## Microservice Based Video to MP3 Converter

This is a microservices-based project in which users can upload video files and get the converted mp3 file back.The flow of the project will be as follows:

As soon as the users make a request, it will first hit our gateway service, which will store the video in MongoDB, then put a message on the queue service. We will be using the RabbitMQ service as a queueing service, letting the downstream service know that there's video to be processed in MongoDB. The video-to-MP3 converter service will consume messages from the queue. It will then get the idea of a video from the message and convert that MongoDB video to mp3, store this mp3 file in MongoDB, and put a new message on the queue to be consumed. This will be consumed by a notification service that will say that the conversion job is done and send an email notification to the client. The client will use the uniquely generated ID acquired from the notification along with his or her JWT token to make a request to the API Gateway to download the mp3 file. The API gateway will pull the mp3 file from MongoDB and serve it to the client.
