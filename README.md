#Categorical DataFrames to Sparse SVM-Light Format
-------------------------------------------------
Converts a categorical design matrix X to a sparse CSR matrix,
then writes to SVM-lite format.

This takes a pandas DataFrame with categorical features, converts category
values to a sparse one-hot representation, then writes the sparse matrix
to SVM-light format.

SVM-light is a text-based format, with one sample per line. It does
not store zero valued features hence is suitable for sparse dataset.

The first element of each line can be used to store a target variable
to predict.

Parameters
----------
X : pandas DataFrame, shape = [n_samples, n_features]
    Training vectors, where n_samples is the number of samples and
    n_features is the number of features.

y : array-like, shape = [n_samples]
    Target values.

filename : string or file-like in binary mode
    If string, specifies the path that will contain the data.
    If file-like, data will be written to f. f should be opened in binary
    mode.

cat_columns: array-like
	List of categorical columns

num_columns: array-like, optional
	List of numerical columns

zero_based : boolean, optional
    Whether column indices should be written zero-based (True) or one-based
    (False).

comment : string, optional
    Comment to insert at the top of the file. This should be either a
    Unicode string, which will be encoded as UTF-8, or an ASCII byte
    string.

query_id : array-like, shape = [n_samples]
    Array containing pairwise preference constraints (qid in svmlight
    format).

Examples
--------

 cat_data1 = ['a','a','b','b','c','c']
cat_data2 = ['12','55','127','55','13','12']
num_data = [1,2,1,1,3,4]
data  = {'catdata1':cat_data1, 'catdata2':cat_data2,'num_data':num_data}
X = pd.DataFrame(data)
y = np.array([1.,0.,1.,1.,0.,0.])
cat_columns = ['catdata1', 'catdata2']
num_columns = ['num_data']

dump_categorical_df_to_svm_light(X, y, 'example', cat_columns, num_columns)

head example	
1.000000 0:1.0000000000000000e+00 8:1.0000000000000000e+00 9:1.0000000000000000e+00
0.000000 0:1.0000000000000000e+00 6:1.0000000000000000e+00 9:2.0000000000000000e+00
1.000000 2:1.0000000000000000e+00 9:2.0000000000000000e+00
1.000000 2:1.0000000000000000e+00 6:1.0000000000000000e+00 9:1.0000000000000000e+00
0.000000 1:1.0000000000000000e+00 7:1.0000000000000000e+00 9:3.0000000000000000e+00
0.000000 1:1.0000000000000000e+00 8:1.0000000000000000e+00 9:4.0000000000000000e+00