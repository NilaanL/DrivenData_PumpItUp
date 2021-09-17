Github Link : https://github.com/NilaanL/DrivenData_PumpItUp.git
# Driven_data_Pump-it-up
https://www.drivendata.org/competitions/7/pump-it-up-data-mining-the-water-table/

Driven Data username   : moracse_170405L
Colab Link : (Note data need to be uploaded)
### Getting Started

Best Score : 0.8141 
Rank : 1985
final moel : CatBoost

![plot](https://github.com/NilaanL/DrivenData_PumpItUp/blob/main/submission%20proof/Best.png)

pre req :
   python 3

1. Clone the project locally 
   ```bash
   https://github.com/NilaanL/DrivenData_PumpItUp.git
   ```
2. Swith to the cloned directory.
   ```bash
   cd DrivenData_PumpItUp
   ```

3. run jupyter lab : open "pump_It.ipynb" in the root directory and run only the subssections mentioned below in the given order
   ```bash
   jupyter lab
   ```
   subsections to run :
      1. Import Libraries
      2. Funtions
      3. read data
      4. Final pipeline

Note : The subsection "Experimenting with data" visualize , explore  and perform diffenrent data cleaning , feature engineering  , feature selection and apply differnt training techniques on the data.


# 1) Data Exploration
> Data imbalance and null value was analysed 
   - functional  ---------------- 32259 
   - non functional ----------- 22824
   - functional needs repair --- 4317

> there were 7 columns with missing values .

   - <b>Column ------------ null_counts</b>
   - funder ------------------- 3635
   - installer ------------------ 3655
   - subvillage ----------------- 371
   - public_meeting ---------- 3334
   - scheme_management --- 3877
   - scheme_name ---------- 28166
   - permit -------------------- 3056

> duplicate columns were identified and removed

Eg  : 
- waterpoint_type  &   waterpoint_type_group      
- 'payment', 'payment_type'

> There were columns with hierachy relationship  this was used to fill null values and later redundant hirachi features were removed 

Eg : 
- extraction_type &  extrcation_type_group & and extraction_type_class
- waterpoint_type_group & waterpoint_type 
- source &  source_type &  source_class
- lga, ward & district_code & region & region code
- recorded_by column is a single value column so not useful for the analysis
- there were offset values in lontitude and latitude columns
- contructed 

> in some columns 0 values represented the missing values 
Eg : 

- latitude
- longtitude 
- construction_year


# 2) Preprocessing

- handle outliers () 
- handle missing values using the mean or median or mode by grouping the near relevant fields availble in the dataset accodingly .
- for the values where the frequnce is less than a threshold in categorical columns were replaced with "others"
- "date_recorded" was conveted to date_Time type.

# 3) new features
- from construction year , and date_recorded new feature "operational_month" ,"operational_year" were created . { assumption was  as the age increase it might need repair}

# 4 ) Encoding 
- categorical features were onhhotencoded and experimented .
- categorical features were labelencoded and experimented .
-  finaly catboost was used to implement the best encoding techniques automaticaly 

# 5 ) Feature selection 

- rfecv (recursive feature eleimination with cross validation ) was used to identify potential features from the availbe 30+ features using Randomeforest as the estimator , 5 fold cross validation  (accuracy ~78% )
- Later from the fetures identified from rfecv diffenrent boosting algorithms were trained ( AdaBoost , XGboost ) 


# 6) Final Model training

- train dataset is divided into train and evluation split with 0.3 split ratio and strified on label.
-  Catboost with los_funtion="MultiClass" was trined by specifying the categorical_columns.
- After the model training , best model was seperated based on "accuracy score" .
- complete traing dataset is retrained on catboost .
- using the best model from catboost test set was predicted .






