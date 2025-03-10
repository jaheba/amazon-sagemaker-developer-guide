# Export<a name="data-wrangler-data-export"></a>

In your Data Wrangler flow, you can export some or all of the transformations that you've made to your data processing pipelines\.

A *Data Wrangler flow* is the series of data preparation steps that you've performed on your data\. In your data preparation, you perform one or more transformations to your data\. Each transformation is done using a transform step\. The flow has a series of nodes that represent the import of your data and the transformations that you've performed\. For an example of nodes, see the following image\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/sagemaker/latest/dg/images/studio/mohave/data-wrangler-destination-nodes-photo-0.png)

The preceding image shows a Data Wrangler flow with two nodes\. The **Source \- sampled** node shows the data source from which you've imported your data\. The **Data types** node indicates that Data Wrangler has performed a transformation to convert the dataset into a usable format\. 

Each transformation that you add to the Data Wrangler flow appears as an additional node\. For information on the transforms that you can add, see [Transform Data](data-wrangler-transform.md)\. The following image shows a Data Wrangler flow that has a **Rename\-column** node to change the name of a column in a dataset\.

You can export your data transformations to the following:
+ Amazon S3
+ SageMaker Pipelines
+ Amazon SageMaker Feature Store
+ Python Code

**Important**  
We recommend that you use the IAM `AmazonSageMakerFullAccess` managed policy to grant AWS permission to use Data Wrangler\. If you don't use the managed policy, you can use an IAM policy that gives Data Wrangler access to an Amazon S3 bucket\. For more information on the policy, see [Security and Permissions](data-wrangler-security.md)\.

When you export your data flow, you're charged for the AWS resources that you use\. You can use cost allocation tags to organize and manage the costs of those resources\. You create these tags for your user\-profile and Data Wrangler automatically applies them to the resources used to export the data flow\. For more information, see [Using Cost Allocation Tags](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/cost-alloc-tags.html)\.

## <a name="data-wrangler-data-export-processing"></a>

Your options for exporting your data transformations depend on to where you're exporting them\. For more information, see the following sections\.

### Export to Amazon S3<a name="data-wrangler-data-export-s3"></a>

Data Wrangler gives you the ability to export your data to a location within an Amazon S3 bucket\. You can specify the location using one of the following methods:
+ Destination node – Where Data Wrangler stores the data after it has processed it\.
+ Export to – Exports the data resulting from a transformation to Amazon S3\.
+ Export data – For small datasets, can quickly export the data that you've transformed\.

Use the following sections to learn more about each of these methods\.

------
#### [ Destination Node ]

If you want to output a series of data processing steps that you've performed to Amazon S3, you create a destination node\. A destination node tells Data Wrangler where to store the data after you've processed it\. After you create a destination node, you create a processing job to output the data\. A processing job is an Amazon SageMaker processing job\. When you're using a destination node, it runs the computational resources needed to output the data that you've transformed to Amazon S3\. 

You can use a destination node to export some of the transformations or all of the transformations that you've made in your Data Wrangler flow\.

You can use multiple destination nodes to export different transformations or sets of transformations\. The following example shows two destination nodes in a single Data Wrangler flow\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/sagemaker/latest/dg/images/studio/mohave/data-wrangler-destination-nodes-photo-4.png)

You can use the following procedure to create destination nodes and export them to an Amazon S3 bucket\.

To export your data flow, you create destination nodes and a Data Wrangler job to export the data\. Creating a Data Wrangler job starts a SageMaker processing job to export your flow\. You can choose the destination nodes that you want to export after you've created them\.

Use the following procedure to create destination nodes\.

1. Choose the **\+** next to the nodes that represent the transformations that you want to export\.

1. Choose **Add destination**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/sagemaker/latest/dg/images/studio/mohave/destination-nodes/destination-nodes-add-destination-0.png)

1. Choose **Amazon S3**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/sagemaker/latest/dg/images/studio/mohave/destination-nodes/destination-nodes-add-destination-S3-selected.png)

1. Specify the fields shown in the following image\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/sagemaker/latest/dg/images/studio/mohave/destination-nodes/destination-nodes-add-destination-configuration.png)

1. Choose **Add destination**\.

Use the following procedure to create a Data Wrangler job\.

Create a job from the **Data flow** page and choose the destination nodes that you want to export\.

1. Choose **Create job**\. The following image shows the pane that appears after you select **Create job**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/sagemaker/latest/dg/images/studio/mohave/destination-nodes/destination-nodes-create-job.png)

1. For **Job name**, specify the name of the export job\.

1. Choose the destination nodes that you want to export\.

1. \(Optional\) Specify a AWS KMS key ARN\. A AWS KMS key is a cryptographic key that you can use to protect your data\. For more information about AWS KMS keys, see [AWS Key Management Service](https://docs.aws.amazon.com/kms/latest/developerguide/overview.html)

1. Choose **Configure job**\. The following image shows the **Configure job** page\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/sagemaker/latest/dg/images/studio/mohave/destination-nodes/destination-nodes-configure-job.png)

1. \(Optional\) Configure the Data Wrangler job\.

1. Choose **Run**\.

------
#### [ Export to ]

As an alternative to using a destination node, you can use the **Export to** option to export your Data Wrangler flow to Amazon S3 using a Jupyter Notebook\. You can choose any data node in your Data Wrangler flow and export it\. Exporting the data node exports the transformation that the node represents and the transformations that precede it\.

Use the following procedure to generate a Jupyter Notebook and run it to export your Data Wrangler flow to Amazon S3\.

1. Choose the **\+** next to the node that you want to export\.

1. Choose **Export to**\.

1. Choose **Amazon S3 \(via Jupyter Notebook\)**\.

1. Run the Jupyter Notebook\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/sagemaker/latest/dg/images/studio/mohave/data-wrangler-destination-nodes-photo-export-to.png)

When you run the notebook, it exports your data flow \(\.flow file\) in the same AWS Region as the Data Wrangler flow\.

------
#### [ Export data ]

If you have a transformation on a small dataset that you want to export quickly, you can use the **Export data** method\. When you start choose **Export data**, Data Wrangler works synchronously to export the data that you've transformed to Amazon S3\. You can't use Data Wrangler until either it finishes exporting your data or you cancel the operation\.

For information on using the **Export data** method in your Data Wrangler flow, see the following procedure\.

To use the **Export data** method\.

1. Choose a node in your Data Wrangler flow by double\-clicking on it\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/sagemaker/latest/dg/images/studio/mohave/export-s3.png)

1. Configure how you want to export the data\.

1. Choose **Export data**\.

------

When you export your data flow to an Amazon S3 bucket, Data Wrangler stores a copy of the flow file in the S3 bucket\. It stores the flow file under the *data\_wrangler\_flows* prefix\. If you use the default Amazon S3 bucket to store your flow files, they use the following naming convention: `sagemaker-region-account number`\. For example, if your account number is 111122223333 and you are using Studio in us\-east\-1, your imported datasets are stored in `sagemaker-us-east-1-111122223333`\. In this example, your \.flow files created in us\-east\-1 are stored in `s3://sagemaker-region-account number/data_wrangler_flows/`\. 

### Export to SageMaker Pipelines<a name="data-wrangler-data-export-pipelines"></a>

When you want to build and deploy large\-scale machine learning \(ML\) workflows, you can use SageMaker Pipelines to create end\-to\-end workflows that manage and deploy SageMaker jobs\. SageMaker Pipelines gives you the ability to build workflows that manage your SageMaker data preparation, model training, and model deployment jobs\. You can use the first\-party algorithms that SageMaker offers by using SageMaker Pipelines\. For more information on SageMaker Pipelines, see [SageMaker Pipelines](https://docs.aws.amazon.com/sagemaker/latest/dg/pipelines.html)\.

When you export one or more steps from your data flow to SageMaker Pipelines, Data Wrangler creates a Jupyter Notebook that you can use to define, instantiate, run, and manage a pipeline\.

#### Use a Jupyter Notebook to Create a Pipeline<a name="data-wrangler-pipelines-notebook"></a>

Use the following procedure to create a Jupyter Notebook to export your Data Wrangler flow to SageMaker Pipelines\.

Use the following procedure to generate a Jupyter Notebook and run it to export your Data Wrangler flow to SageMaker Pipelines\.

1. Choose the **\+** next to the node that you want to export\.

1. Choose **Export to**\.

1. Choose **SageMaker Pipelines \(via Jupyter Notebook\)**\.

1. Run the Jupyter Notebook\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/sagemaker/latest/dg/images/studio/mohave/data-wrangler-destination-nodes-photo-export-to.png)

The Jupyter Notebook that Data Wrangler produces can be used to define a pipeline\. The pipeline includes the data processing steps that are defined by your Data Wrangler flow\. 

You can add additional steps to your pipeline by adding steps to the `steps` list in the following code in the notebook:

```
pipeline = Pipeline(
    name=pipeline_name,
    parameters=[instance_type, instance_count],
    steps=[step_process], #Add more steps to this list to run in your Pipeline
)
```

For more information on defining pipelines, see [Define SageMaker Pipeline](https://docs.aws.amazon.com/sagemaker/latest/dg/define-pipeline.html)\.

### Export to Python Code<a name="data-wrangler-data-export-python-code"></a>

To export all steps in your data flow to a Python file that you can manually integrate into any data processing workflow, use the following procedure\.

Use the following procedure to generate a Jupyter Notebook and run it to export your Data Wrangler flow to Python Code\.

1. Choose the **\+** next to the node that you want to export\.

1. Choose **Export to**\.

1. Choose **Python Code**\.

1. Run the Jupyter Notebook\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/sagemaker/latest/dg/images/studio/mohave/data-wrangler-destination-nodes-photo-export-to.png)

You might need to configure the Python script to make it run in your pipeline\. For example, if you're running a Spark environment, make sure that you are running the script from an environment that has permission to access AWS resources\.

### Export to Amazon SageMaker Feature Store<a name="data-wrangler-data-export-feature-store"></a>

You can use Data Wrangler to export features you've created to Amazon SageMaker Feature Store\. A feature is a column in your dataset\. Feature Store is a centralized store for features and their associated metadata\. You can use Feature Store to create, share, and manage curated data for machine learning \(ML\) development\. Centralized stores make your data more discoverable and reusable\. For more information about Feature Store, see [Amazon SageMaker Feature Store](https://docs.aws.amazon.com/sagemaker/latest/dg/feature-store.html)\.

A core concept in Feature Store is a feature group\. A feature group is a collection of features, their records \(observations\), and associated metadata\. It's similar to a table in a database\.

You can use Data Wrangler to do one of the following:
+ Update an existing feature group with new records\. A record is an observation in the dataset\.
+ Create a new feature group from a node in your Data Wrangler flow\. Data Wrangler adds the observations from your datasets as records in your feature group\.

If you're updating an existing feature group, your dataset's schema must match the schema of the feature group\. All the records in the feature group are replaced with the observations in your dataset\.

You can use either a Jupyter Notebook or a destination node to update your feature group with the observations in the dataset\.

------
#### [ Destination Node ]

If you want to output a series of data processing steps that you've performed to a feature group, you can create a destination node\. When you create and run a destination node, Data Wrangler updates a feature group with your data\. You can also create a new feature group from the destination node UI\. After you create a destination node, you create a processing job to output the data\. A processing job is an Amazon SageMaker processing job\. When you're using a destination node, it runs the computational resources needed to output the data that you've transformed to the feature group\. 

You can use a destination node to export some of the transformations or all of the transformations that you've made in your Data Wrangler flow\.

Use the following procedure to create a destination node to update a feature group with the observations from your dataset\.

To update a feature group using a destination node, do the following\.

1. Choose the **\+** symbol next to the node containing the dataset that you'd like to export\.

1. Under **Add destination**, choose **SageMaker Feature Store**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/sagemaker/latest/dg/images/studio/mohave/feature-store-destination-node-selection.png)

1. Double click on the feature group\. Data Wrangler checks whether the schema of the feature group matches the schema of the data that you're using to update the feature group\.

1. \(Optional\) Select **Export to offline store only** for feature groups that have both an online store and an offline store\. This option only updates the offline store with observations from your dataset\.

1. After Data Wrangler validates the schema of your dataset, choose **Add**\.

Use the following procedure to create a new feature group with data from your dataset\.

You can have the following options for how you want to store your feature group:
+ Online – Low latency, high availability cache for a feature group that enables real\-time lookup of records\. The online store allows quick access to the latest value for a record in a feature group\.
+ Offline – Stores data for your feature group in an Amazon S3 bucket\. You can store your data offline when you don't need low latency \(sub\-second\) reads\. You can use an offline store for features used in data exploration, model training, and batch inference\.
+ Both online and offline – Stores your data in both an online store and an offline store\.

To create a feature group using a destination node, do the following\.

1. Choose the **\+** symbol next to the node containing the dataset that you'd like to export\.

1. Under **Add destination**, choose **SageMaker Feature Store**\.

1. Choose **Create Feature Group**\.

1. In the following dialog box, if your dataset doesn't have an event time column, select **Create "EventTime" column**\.

1. Choose **Next**\.

1. Choose **Copy JSON Schema**\. When you create a feature group, you paste the schema into the feature definitions\.

1. Choose **Create**\.

1. For **Feature group name**, specify a name for your feature group\.

1. For **Description \(optional\)**, specify a description to make your feature group more discoverable\.

1. To create a feature group for an online store, do the following\.

   1. Select **Enable storage online**\.

   1. For **Online store encryption key**, specify an AWS managed encryption key or an encryption key of your own\.

1. To create a feature group for an offline store, do the following\.

   1. Select **Enable storage offline**\.

   1. Specify values for the following fields:
      + **S3 bucket name** – The name of the bucket storing the feature group\.
      + **\(Optional\) Dataset directory name** – The Amazon S3 prefix that you're using to store the feature group\.
      + **IAM Role ARN** – The IAM role that has access to feature store\.
      + **Offline store encryption key** – By default, Feature Store uses an AWS managed key, but you can use the field to specify a key of your own\.

1. Choose **Continue**\.

1. Choose **JSON**\.

1. Remove the placeholder brackets in the window\.

1. Paste the JSON text from Step 6\.

1. Choose **Continue**\.

1. For **RECORD IDENTIFIER FEATURE NAME**, choose the column in your dataset that has unique identifiers for each record in your dataset\.

1. For **EVENT TIME FEATURE NAME**, choose the column with the timestamp values\.

1. Choose **Continue**\.

1. \(Optional\) Add tags to make your feature group more discoverable\.

1. Choose **Continue**\.

1. Choose **Create feature group**\.

1. Navigate back to your Data Wrangler flow and choose the refresh icon next to the **Feature Group** search bar\.

**Note**  
If you've already created a destination node for a feature group within a flow, you can't create another destination node for the same feature group\. If you want to create another destination node for the same feature group, you must create another flow file\.

Use the following procedure to create a Data Wrangler job\.

Create a job from the **Data flow** page and choose the destination nodes that you want to export\.

1. Choose **Create job**\. The following image shows the pane that appears after you select **Create job**\.

1. For **Job name**, specify the name of the export job\.

1. Choose the destination nodes that you want to export\.

1. \(Optional\) Specify a AWS KMS key ARN\. A AWS KMS key is a cryptographic key that you can use to protect your data\. For more information about AWS KMS keys, see [AWS Key Management Service](https://docs.aws.amazon.com/kms/latest/developerguide/overview.html)

1. Choose **Configure job**\. The following image shows the **Configure job** page\.

1. \(Optional\) Configure the Data Wrangler job\.

1. Choose **Run**\.

------
#### [ Jupyter Notebook ]

Use the following procedure to a Jupyter Notebook to export to Amazon SageMaker Feature Store\.

Use the following procedure to generate a Jupyter Notebook and run it to export your Data Wrangler flow to Feature Store\.

1. Choose the **\+** next to the node that you want to export\.

1. Choose **Export to**\.

1. Choose **Amazon SageMaker Feature Store \(via Jupyter Notebook\)**\.

1. Run the Jupyter Notebook\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/sagemaker/latest/dg/images/studio/mohave/data-wrangler-destination-nodes-photo-export-to.png)

Running a Jupyter Notebook runs a Data Wrangler job\. Running a Data Wrangler job starts a SageMaker processing job\. The processing job ingests the flow into an online and offline feature store\.

**Important**  
The IAM role you use to run this notebook must have the following AWS managed policies attached: `AmazonSageMakerFullAccess` and `AmazonSageMakerFeatureStoreAccess`\.

You only need to enable one online or offline feature store when you create a feature group\. You can also enable both\. To disable online store creation, set `EnableOnlineStore` to `False`:

```
# Online Store Configuration
online_store_config = {
    "EnableOnlineStore": False
}
```

The notebook uses the column names and types of the dataframe you export to create a feature group schema, which is used to create a feature group\. A feature group is a group of features defined in the feature store to describe a record\. The feature group defines the schema and features contained in the feature group\. A feature group definition is composed of a list of features, a record identifier feature name, an event time feature name, and configurations for its online store and offline store\. 

Each feature in a feature group can have one of the following types: *String*, *Fractional*, or *Integral*\. If a column in your exported dataframe is not one of these types, it defaults to `String`\. 

The following is an example of a feature group schema\.

```
column_schema = [
    {
        "name": "Height",
        "type": "long"
    },
    {
        "name": "Input",
        "type": "string"
    },
    {
        "name": "Output",
        "type": "string"
    },
    {
        "name": "Sum",
        "type": "string"
    },
    {
        "name": "Time",
        "type": "string"
    }
]
```

Additionally, you must specify a record identifier name and event time feature name:
+ The *record identifier name* is the name of the feature whose value uniquely identifies a record defined in the feature store\. Only the latest record per identifier value is stored in the online store\. The record identifier feature name must be one of feature definitions' names\.
+ The *event time feature name* is the name of the feature that stores the `EventTime` of a record in a feature group\. An `EventTime` is a point in time when a new event occurs that corresponds to the creation or update of a record in a feature\. All records in the feature group must have a corresponding `EventTime`\.

The notebook uses these configurations to create a feature group, process your data at scale, and then ingest the processed data into your online and offline feature stores\. To learn more, see [Data Sources and Ingestion](https://docs.aws.amazon.com/sagemaker/latest/dg/feature-store-ingest-data.html)\.

------

The notebook uses these configurations to create a feature group, process your data at scale, and then ingest the processed data into your online and offline feature stores\. To learn more, see [Data Sources and Ingestion](https://docs.aws.amazon.com/sagemaker/latest/dg/feature-store-ingest-data.html)\.