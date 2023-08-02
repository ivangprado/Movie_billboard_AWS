# Movie_billboard_AWS

In this project, I build an application in the AWS Cloud that queries the TMDB movie billboard through API calls. The result of these queries will be stored in S3. Additionally, the most relevant data will be stored in DynamoDB, allowing for future queries via an API built on top of Lambda functions.

![image](https://github.com/ivangprado/Movie_billboard_AWS/assets/6001254/1f8e3d00-b834-4aec-a780-f8c50bf0b27e)

### Steps

1. I create a lambda function that makes TMDB API calls to get the movies that are currently in theaters. The information for these movies is stored on S3 with the path: ID_MOVIE/YEAR_MONTH_DAY.json. For this function, I need to add the request library dependency as a layer. It will run automatically every 24 hours.

![image](https://github.com/ivangprado/Movie_billboard_AWS/assets/6001254/7652fb68-1dda-4ad0-92b8-c058689c6c67)

2. Another lambda function is created that will be automatically executed when a new file is stored in S3. This function stores the information in DynamoDB. It also adds some additional fields to the information obtained through the API to see the evolution of the movie ranking over time.

![image](https://github.com/ivangprado/Movie_billboard_AWS/assets/6001254/132c0bf7-39da-41f8-9f69-fcfc450c0d01)

3. A new lambda is created that is called by an endpoint created in AWS API Gateway. The lambda receives a year and a month and returns a list of movies for that year and month to the API Gateway.

4. Another lambda is created that is called by another AWS API Gateway resource. This time, the lambda receives a movie ID and returns the information for that movie to the API Gateway.

5. Finally, the API implemented in API Gateway is tested with a widget created with ipywidgets.

