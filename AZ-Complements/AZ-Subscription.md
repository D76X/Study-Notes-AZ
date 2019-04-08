# AZ Complements - Subscription

## Main Resources

1. [Managing Microsoft Azure Subscriptions by Dan Lachance](https://app.pluralsight.com/library/courses/microsoft-azure-subscriptions-managing/table-of-contents)  

2. [Mastering Microsoft Azure Resource Manager by James Bannan](https://app.pluralsight.com/library/courses/microsoft-azure-resource-manager-mastering/table-of-contents) 

## Realted Resources



## Complementary Resources

---

### [Leaning Goals](https://app.pluralsight.com/player?course=microsoft-azure-subscriptions-managing&author=daniel-lachance&name=c3476341-be05-442d-bf0a-4804e866e37d&clip=0&mode=live)  

- Azure Resource Tagging
- Azure cost budgeting and tracking
- Azure role assignments
- Azure resource providers
- Tools to track and reduce Azure costs
- How to control resource deployment and management through **Role-based Access Control (RBAC)** and **Azure Policies**
- How to register **Azure Resource Providers** to enhance Azure functionality

---

### Main Subjects

1. **Configure Microsoft Azure Policies** to control what type of resources can be controlled and managed.
2. **Configure Cost Spending Limits and Tagging**.
3. **Role-base Access Control (RBAC)** as sets of permissions assigned to roles.
4. **Manage Microsoft Azure Resource Providers** ot be able to deploy Azure resources.

---

## [Configure Microsoft Azure Policies](https://app.pluralsight.com/player?course=microsoft-azure-subscriptions-managing&author=daniel-lachance&name=2bd06ed4-f0c8-4b8d-89d9-1896675d4e57&clip=0&mode=live)  

- Resource Tagging and how to tag resources.
- [What Tags are in Azure and why we would use them](https://app.pluralsight.com/player?course=microsoft-azure-subscriptions-managing&author=daniel-lachance&name=2bd06ed4-f0c8-4b8d-89d9-1896675d4e57&clip=1&mode=live).
- How to use Azure Portal **All Services** pane to filter on Tags.
- What **Microsoft Azure Policies are and why they are used.**.
- Azure Policy initiative definitions.
- Exclusion scopes.
- Built-in & csutom policies.

#### Summary

- Tags are **key-value pairs** that can be added to resources including resource groups.
- Tags can be used to logically and systemmatically organize resources and easily search and find them.
- Tags **can be applied to Resource Groups**.
- Tags are **metadata that is not inherited** thus the resources that are in a tagged resource goroup do not have their RG's tags.
- There is alimit of 15 tags that can be applied to any resource. 
- Tags can be added at creation time or after creation with Powershel/Azure CLI while with the Azure Portal only after creation of te resource.

---

## Demos

- [Tag Resources in the Azure Portal](https://app.pluralsight.com/player?course=microsoft-azure-subscriptions-managing&author=daniel-lachance&name=2bd06ed4-f0c8-4b8d-89d9-1896675d4e57&clip=2&mode=live)  

- [Tag Resources with Powershell](https://app.pluralsight.com/player?course=microsoft-azure-subscriptions-managing&author=daniel-lachance&name=2bd06ed4-f0c8-4b8d-89d9-1896675d4e57&clip=3&mode=live)

```
# get all the tags defined in the subscription
Get-AzureRmTag
```

```
# use the set of Resource Manager (RM) cmdlets 
# read all the tags for a resource
(Get-AzureRmResource -ResourceName "MyUbuntuVM1" -ResourceGroupName "RG1").Tags
```

```
# use variables
# use the set of Resource Manager (RM) cmdlets 
# read all the tags for a resource
$r = Get-AzureRmResource -ResourceName "MyUbuntuVM1" -ResourceGroupName "RG1"
$tags = $r.Tags

# must add to tags otherwise the property value is replaced!
$tags += @{Dept="IT"; Phase="Testing"}
Set-AzureRmResource -ResourceId $r.Id -Tags $tags -Force
```

```
# remove all tags on a resource
Set-AzureRmResource $r.Id -Tag @{} -Force
```

```
# gets all the resources in the subsciption with a specific tag
Get-AzureRmResource -TagName Dept

# get the names of all reosurces that have the tag defined as the -Tag option
(Get-AzureRmResource -Tag @{Dept="IT"}).Name
```

---

