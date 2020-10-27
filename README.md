Audit Azure subscription RBAC assignments
=========================================

            

If you need to audit/log Azure permissions, this is it. I created this script to help perform a RBAC audit for a Azure subscription. This script resolves all RBAC assignments, then expand every group to retain only resolved users. 


It is build so that you can take the output and do whatever you want with it after, whenever it's convert it to JSON, CSV, XML.


 


Here are 2 invocation examples and their outputs


 

Usage
 


PowerShell
Edit|Remove
powershell
Connect-AzureRmAccount

Set-AzureRmContext -Subscription 'Your Subscription'

# Perform an audit grouped by users
$rbacAudit = Invoke-AzureRmSubscriptionRBACAudit.ps1 

#output the result as-is
$rbacAudit

Id                       : 4506482f-23a0-4820-850b-06219f704739
DisplayName        : FirstName1 LastName1
ParentGroup         : {Id, DisplayName}
RoleDefinitionName : Reader
Scope                  : /subscriptions/11111111-1111-1111-1111-111111111111
CanDelegate        : False

Id                 : dc37e4bd-1811-4b5e-ba5e-1322ff5ac29d
DisplayName        : FirstName2 LastName2
ParentGroup        : {Id, DisplayName}
RoleDefinitionName : Owner
Scope              : /subscriptions/11111111-1111-1111-1111-111111111111
CanDelegate        : False

Id                 : 8a173eb5-52a4-4a5b-b6ae-aefc3dac7489
DisplayName        : FirstName3 LastName3
ParentGroup        : {Id, DisplayName}
RoleDefinitionName : Reader
Scope              : /subscriptions/11111111-1111-1111-1111-111111111111/resourceGroups/stg
CanDelegate        : False

Id                 : 4e13ae9c-7e3b-49e4-a49e-e81c2dd21151
DisplayName        : FirstName4 LastName4
ParentGroup        : {Id, DisplayName}
RoleDefinitionName : Contributor
Scope              : /subscriptions/11111111-1111-1111-1111-111111111111/resourceGroups/stg/providers/Microsoft.Insights/components/stg-ai-app-qjkgqezdtfjr4
CanDelegate        : False

#output the result as JSON
$rbacAudit | ConvertTo-Json -Depth 5

[
    {
        'Id':  '4506482f-23a0-4820-850b-06219f704739',
        'DisplayName':  'FirstName1 LastName1',
        'ParentGroup':  {
                            'Id':  '9cb7e0c1-0513-441b-b484-8b55761694fe',
                            'DisplayName':  'SecurityGroupName1'
                        },
        'RoleDefinitionName':  'Reader',
        'Scope':  '/subscriptions/11111111-1111-1111-1111-111111111111',
        'CanDelegate':  false
    },
    ...]

Connect-AzureRmAccount 
 
Set-AzureRmContext -Subscription 'Your Subscription' 
 
# Perform an audit grouped by users 
$rbacAudit = Invoke-AzureRmSubscriptionRBACAudit.ps1  
 
#output the result as-is 
$rbacAudit 
 
Id                       : 4506482f-23a0-4820-850b-06219f704739 
DisplayName        : FirstName1 LastName1 
ParentGroup         : {Id, DisplayName} 
RoleDefinitionName : Reader 
Scope                  : /subscriptions/11111111-1111-1111-1111-111111111111 
CanDelegate        : False 
 
Id                 : dc37e4bd-1811-4b5e-ba5e-1322ff5ac29d 
DisplayName        : FirstName2 LastName2 
ParentGroup        : {Id, DisplayName} 
RoleDefinitionName : Owner 
Scope              : /subscriptions/11111111-1111-1111-1111-111111111111 
CanDelegate        : False 
 
Id                 : 8a173eb5-52a4-4a5b-b6ae-aefc3dac7489 
DisplayName        : FirstName3 LastName3 
ParentGroup        : {Id, DisplayName} 
RoleDefinitionName : Reader 
Scope              : /subscriptions/11111111-1111-1111-1111-111111111111/resourceGroups/stg 
CanDelegate        : False 
 
Id                 : 4e13ae9c-7e3b-49e4-a49e-e81c2dd21151 
DisplayName        : FirstName4 LastName4 
ParentGroup        : {Id, DisplayName} 
RoleDefinitionName : Contributor 
Scope              : /subscriptions/11111111-1111-1111-1111-111111111111/resourceGroups/stg/providers/Microsoft.Insights/components/stg-ai-app-qjkgqezdtfjr4 
CanDelegate        : False 
 
#output the result as JSON 
$rbacAudit | ConvertTo-Json -Depth 5 
 
[ 
    { 
        'Id':  '4506482f-23a0-4820-850b-06219f704739', 
        'DisplayName':  'FirstName1 LastName1', 
        'ParentGroup':  { 
                            'Id':  '9cb7e0c1-0513-441b-b484-8b55761694fe', 
                            'DisplayName':  'SecurityGroupName1' 
                        }, 
        'RoleDefinitionName':  'Reader', 
        'Scope':  '/subscriptions/11111111-1111-1111-1111-111111111111', 
        'CanDelegate':  false 
    }, 
    ... ]



Requirements

Tested with AzureRM.Resources Version 5.x, & 6.x


        
    
TechNet gallery is retiring! This script was migrated from TechNet script center to GitHub by Microsoft Azure Automation product group. All the Script Center fields like Rating, RatingCount and DownloadCount have been carried over to Github as-is for the migrated scripts only. Note : The Script Center fields will not be applicable for the new repositories created in Github & hence those fields will not show up for new Github repositories.
