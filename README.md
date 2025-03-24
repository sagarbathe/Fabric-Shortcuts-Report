# Fabric-Shortcuts-Report

** Creating a new repo instead of updating the old one.
Few updates made from the previous repo
- This new repo uses wrapper functions from Semantic Link Labs (https://github.com/microsoft/semantic-link-labs). Using the wrapper functions, reduces the code complexity and makes it much easier to maintain.
- Storing both internal and external shortcuts in one table
- Created a new report for listing duplicate shortcuts across the Fabric tenant. Definition of a duplicate shortcut is : A shortcut created in the same lakehouse and workspace and pointing to the same source (Source can 
  be internal such as Onelake lakehouse, warehouse or KQL table or external such as same ADLS or S3 path)

****************
Objective:

Currently, there is no way in Fabric to show details of all the shortcuts created in workspaces and lakehouses. The objective of this project is to capture this information via the Fabric Shortcut REST APIs and use Power BI to visualize this information

This repo will consist of a notebook and Power BI report sample. The notebook captures metadata about all the shortcuts across all lakehouses and workspaces in your Fabric tenant. 

Prerquisites:
- This notebook currently supports running as a Fabric Admin user. Service Prinicipal support is available for Shortcut Fabric APIs but not for the semantic link labs wrapper functions. I will provide a new 
  notebook for Service Prinicipal support when it is supported
- To capture shortcuts for all capacities and workspace, ensure the capacities are active. If a capacity is not active, shortcuts in lakehouses and workspaces attached to those capacities won't be captured. Once 
  the notebook is executed successfully, capacities can be paused (except the one where the Power BI report will use)

Steps:

- Import the notebook 'GetFabricShortcuts_semanticlinklabs.ipynb' in the workspace of your choice.
- Follow all the instructions in the notebook. After successful completion of the notebook, 2 delta tables (ShortcutsMetadata_semanticlinklabs and ShortcutsMetadata_dups_semanticlinklabs) will be created in the 
  lakehouse you had specified in the notebook
- Create a custom semantic model (dataset) called 'sm_ShortcutsMetadata_semlinklabs' in the lakehouse you had selected in the notebook. Include the 2 tables mentioned above in the semantic model
- Import the Power BI report 'Fabric Workspace Shortcut Details_semlinklabs' in Power BI desktop. Ensure you are logged in as same user as in Fabric. You should see a pop-up that report is not able to find the 
  dataset. Click on Edit and select semantic model (dataset) created 
  in the previous step. Save and publish the report in the workspace you saved the notebook and semantic model earlier. Now you should be able to open the report in Fabric and use it

PowerBI Report screenshots:
Summary -
![image](https://github.com/user-attachments/assets/a31b365a-fa93-412a-8f0a-b60503979209)

Internal Shortcuts -
![image](https://github.com/user-attachments/assets/225869f8-4394-4669-8957-3ebddca47eb1)

External Shortucts -
![image](https://github.com/user-attachments/assets/21dac989-eb8e-48dd-90ae-2b75f5fcaf22)


