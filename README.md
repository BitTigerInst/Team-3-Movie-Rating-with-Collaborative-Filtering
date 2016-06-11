# Movie Rating with Collaborative Filtering
## Description
Recommender Systems play an important role in information and e-commerce ecosystem. They provide a powerful method for enabling users to filter through large information and product spaces. In this project, we will build up a server recommending movies to a user, with utilizing Apache Spark and a subset dataset of 500,000 ratings  from the movielens 10M stable benchmark rating dataset.

At the same time, we will use User-user Collaborative Filtering to set up a model for the movie ranking prediction. User–user Collaborative Filtering is a straightforward algorithmic interpretation of the core premise of collaborative filtering: find other users whose past rating behavior is similar to that of the current user and use their ratings on other items to predict what the current user will like. 

## Plan
###Todo List
- Data Preparation. We will separate our original dataset into training dataset, validation dataset and test dataset.
- Model Training and Selection. We will develop different models. Use training dataset and validation dataset for model training, calculating the Root Mean Square Error to compute the error of each model. Select the best model based on RMSE.
- Model Evaluation. Apply the best model to the test dataset to decide how good our model is.

### Time Schedule
| Stage | Start      | End        | Goals                                                                                                            |
|-------|------------|------------|------------------------------------------------------------------------------------------------------------------|
| 1     | 06/14/2016 | 06/20/2016 | Get to know Recommender System and user-user CF. Set up Apache Spark Environment and familiar with MLib in Scala |
| 2     | 06/21/2016 | 06/27/2016 | Multiple models developing                                                                                       |
| 3     | 06/28/2016 | 07/04/2016 | Models training and,validating                                                                                   |
| 4     | 07/05/2016 | 07/11/2016 | Select the Best model and test                                                                                   |
| 5     | 07/12/2016 | 07/18/2016 | Finish project report and demo video                                                                             |

## License
This project is distributed under the [MIT liscense](https://github.com/BitTigerInst/Team-3-Movie-Rating-with-Collaborative-Filtering/blob/master/LICENSE.md)
## Resourse
- [Collaborating Filtering Recommender System, 2010, Michael D. Ekstrand](http://files.grouplens.org/papers/FnT%20CF%20Recsys%20Survey.pdf)
- [BitTiger Movie Rating](https://www.bittiger.io/microproject/ffunnGadBsofxdQsJ)
- [MovieLens](http://grouplens.org/datasets/movielens/)
- [Spark](http://spark.apache.org)

##Project Information
- Category: Data Analysis
- Team: Team 3
- Description:  Build up a model of high-correctness to recommend movies to a user
- Stack: Apache Spark
