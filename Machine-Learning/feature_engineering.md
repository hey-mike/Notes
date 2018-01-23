# Feature Engineering


## Identifying Important Features In Random Forests

NOTE:  there are two things to keep in mind regarding feature importance:

- While not technically required, scikit-learn requires that we break up nominal categorical features into multiple binary features. This has the effect of spreading the importance of that feature across all of the bninary features and can often makes each feature appear to be *umimportant* even when the original nominal categorical feature is highly imprtant
- If two features are highly correlated then one feature will claim much of the importance, making the other feature appear to be far less important, which has implications for interpretation if not considerred.

