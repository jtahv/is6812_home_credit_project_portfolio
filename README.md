# IS 6812 Home Credit Default Risk portfolio

## Getting started
Home Credit hosted this competition on Kaggle (https://www.kaggle.com/competitions/home-credit-default-risk) back in 2018. Even after six years, it remains a great problem for students and others interested in data science to try solving to this day.

For me, the preparation for the project began just like any other project: getting familiar with the objective, understanding the available data, and starting to brainstorm possible solutions. I wouldn't say I was excited to start working on such a big project, but I was pleasantly surprised that the topic would be something I personally have a lot of knowledge about, as I work in lending—specifically in subprime lending, where consumers often don’t have the best credit situations. More on that in a bit.

## Business problem
Once I had a solid understanding of the problem, I wrote a business problem statement. The business problem statement is included in this repository, but to briefly summarize: Home Credit is facing challenges in accurately qualifying customers who lack some of the traditional credit qualification factors, such as credit scores or credit history. They aim to use alternative data sources for customer qualification. However, with their current methods, they risk taking on unnecessary liabilities, while also potentially missing out on good customers.

## Analytics approach
My team and I attempted to use a variety of machine learning methods to predict customers' repayment abilities. In total, we experimented with four different machine learning methods: neural networks, gradient boosting, random forests, and decision trees. We applied several techniques to each model, including but not limited to class balancing, feature selection through variable importance (using Random Forest and PCA), feature engineering by incorporating additional data sources, and hyperparameter tuning within the models.

The primary goal of this project was to predict whether a customer would have difficulty repaying the loan, as indicated by the binary variable 'target' provided by Home Credit.

## Benefit of a solution
The benefit of a model that can predict whether a customer might have issues repaying a loan is substantial. Currently, in the data provided by Home Credit, about 8% of customers experienced issues repaying their loans. This means that if Home Credit decided to approve all loans, approximately 8% of them would face challenges.

Let’s make some assumptions here. Suppose Home Credit approved 5,000 loan applications with an average loan size of $100,000. That would result in a portfolio of $500 million. If 8% of that portfolio encounters repayment challenges, that’s $40 million at risk. Home Credit does not clearly define what target = 1 means in their dataset, but that $40 million could represent potential defaults, charge-offs, or recovery-related costs (e.g., selling loans to collections, bankruptcy operations, internal recovery costs). This is a significant loss that could potentially be avoided with a more accurate machine learning model.

Of course, these numbers are high-level assumptions, and the actual situation may vary slightly, but this example provides a clear idea of the potential benefits.

## Approach to Data Analysis (EDA)
As I briefly mentioned, I work for a company that operates in a subprime lending environment. I currently work on the BI (Business Intelligence) side, but I’m somewhat familiar with our predictive models as well. I obviously can’t go into details about those models, but to provide a simple description: they are extremely complex! With that in mind, I knew that building a good model for credit prediction would require a certain level of complexity, and that alternative data would likely play a significant role.

My EDA started with analyzing the 'main' dataset provided by Home Credit, application_train, which included numerous features about applicants, such as their education, employment, and living-related information. The main dataset had over 100 columns, so there was a lot to review. My primary goal was to identify variables that might have predictive power over the target variable.

Once I identified some possible predictors, I shifted focus to the alternative data. Based on my experience, I knew that credit-related variables (provided in the bureau.csv file) might offer valuable insights. To my surprise, I discovered that the majority of applicants in the dataset had records in the bureau table. I decided that aggregating the bureau table and creating new variables based on tradelines (credit accounts) would be a good approach.

After creating new variables to join with application_train, I conducted additional EDA to confirm their predictive potential. To my surprise, I observed some correlation between these new variables and the target variable—not a strong correlation, but enough to proceed to the next step.

## Modeling
After completing the EDA (done as an individual assignment), it was time for group work. We decided to start our group modeling process by each running our own models. I chose XGBoost. Although I wasn’t very familiar with XGBoost, I interact with Data Scientists at work quite frequently, and they often discuss its applications. Moreover, it’s one of the most commonly used modeling techniques in the industry today, so I decided to give it a try.

The initial models didn’t perform very well. The data imbalance posed challenges, and even after trying to balance the data using undersampling, the results were still not great. This was largely because I didn’t experiment with enough hyperparameter combinations, primarily due to insufficient time.

It wasn’t until after we had submitted the group modeling notebook that I truly started fine-tuning the model. I used the dataExplorer package to conduct additional EDA, uncover trends in the data, and perform feature selection based on my findings. Then, I retrained the model using the caret package. I employed a parameter grid to test various hyperparameter combinations, totaling about 2,800 iterations. Model training took approximately 9 hours, but once complete, it was the best model I had built so far, achieving an AUC of around 0.74. While still not excellent, it was an improvement.

## Business value of the solution
My best model achieved a Kaggle score of about 0.68 (despite an in-sample AUC score of over 0.74). As a group, our best model—a neural network—achieved an AUC of 0.72. I believe the team that won the Kaggle competition had a score of 0.805. That said, while our solution might not provide the best value for Home Credit, with further fine-tuning, I believe it could be competitive.

## Difficulties faced as a group
One of the primary challenges we faced as a group was time. All of us are working professionals, so finding time for a school project wasn’t always feasible or a top priority. In a graduate school setting, group projects can be particularly challenging, as students often have busier lives compared to undergraduate settings.

Another difficulty was combining our code. Each team member has a unique coding style, and while merging the code wasn’t inherently difficult, it was time-consuming.

## My contribution to the project
As I discusssed above, I did pretty extensive EDA and feature engineering in preparation for modeling. Once it was time to put all of our work together, we ended up using all of my modifications for each of the models, so whether the model performed well or poorly, a lot of that would probably be my fault.

## What did I learn from this project
You can always do more.

What do I mean by that? As I noted in several of my project assignments, additional EDA and feature engineering could have opened new doors. From my observations at work, data science projects undertaken by our Data Scientists often take weeks or even months. Given that a work project involves roughly 40 hours per week compared to maybe 10 hours per week for a school project, it’s clear how much effort can go into building a truly effective data science solution.
