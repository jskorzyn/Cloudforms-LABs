# Lab Introduction

<!-- TOC -->

- [Lab Introduction](#lab-introduction)
    - [Introduction to CloudForms](#introduction-to-cloudforms)
        - [Access the lab environment](#access-the-lab-environment)
    - [Verify Lab](#verify-lab)
        - [OpenStack Provider status](#openstack-provider-status)
        - [Red Hat Virtualization Provider status](#red-hat-virtualization-provider-status)
        - [Red Hat OpenShift Container Platform status](#red-hat-openshift-container-platform-status)
    - [CloudForms with Ansible batteries included](#cloudforms-with-ansible-batteries-included)
        - [Introduction to Ansible](#introduction-to-ansible)
        - [Value provided by a Service Catalog](#value-provided-by-a-service-catalog)
        - [Service Basics](#service-basics)
        - [Power on target VM](#power-on-target-vm)
        - [Make sure embedded Ansible role is enabled and running](#make-sure-embedded-ansible-role-is-enabled-and-running)
        - [Add a Git repository of Ansible Playbooks](#add-a-git-repository-of-ansible-playbooks)
        - [Store Virtual Machine Credentials](#store-virtual-machine-credentials)
        - [Create an Ansible Service Catalog](#create-an-ansible-service-catalog)
        - [Create a Service Catalog Item](#create-a-service-catalog-item)
        - [Test the Service Catalog Item](#test-the-service-catalog-item)
    - [Add a button to a Virtual Machine](#add-a-button-to-a-virtual-machine)
        - [Add a Button Group](#add-a-button-group)
        - [Add a new Button to the Button Group](#add-a-new-button-to-the-button-group)
        - [Test the Ansible Button Customization](#test-the-ansible-button-customization)
    - [Improve the Service Dialog](#improve-the-service-dialog)
        - [Edit the Service Dialog](#edit-the-service-dialog)
        - [Create improved Service Catalog Item](#create-improved-service-catalog-item)
        - [Update the Button definition](#update-the-button-definition)
        - [Test the improved Button](#test-the-improved-button)
    - [Build a Service Catalog to create and delete users](#build-a-service-catalog-to-create-and-delete-users)
        - [Create a Service Catalog Item for the Playbook](#create-a-service-catalog-item-for-the-playbook)
        - [Order the "create user" Service Catalog Item](#order-the-create-user-service-catalog-item)
        - [Monitor create user Playbook execution](#monitor-create-user-playbook-execution)
        - [Verify Playbook results](#verify-playbook-results)
    - [Advanced labs](#advanced-labs)
        - [Use the Self Service user Interface](#use-the-self-service-user-interface)
        - [Build a button to execute remote commands](#build-a-button-to-execute-remote-commands)
            - [The use case](#the-use-case)
            - [Service Dialog](#service-dialog)
            - [Service Catalog Item](#service-catalog-item)
            - [Button](#button)
            - [Improve it further](#improve-it-further)
            - [Need Help?](#need-help)
    - [Even more?](#even-more)

<!-- /TOC -->

## Introduction to CloudForms

[Red Hat CloudForms](http://www.redhat.com/cloudforms) is an infrastructure management platform that offers a consistent way to track costs, control resource allocation, and ensure compliance across all your networked environments. Manage Virtual Machines, containers, and your clouds in the same way with a single tool.

In this lab we will focus on he Ansible features provided by CloudForms. We will setup the embedded Ansible role, create Service Catalog Items for Ansible Playbooks, and demonstrate how the CloudForms UI can be exteded with custom menus and buttons.


### Access the lab environment



## Verify Lab

Let's start by verifying the status of all providers. Use the URL as desplained before and the provided login credentials.

![CloudForms login page](../../common/img/cloudforms-login-page.png)

In CloudForms we can add so called "Providers". Providers are categorized into Cloud, Infrastructure, Physical and Container Providers. CloudForms 4.6 supports the following list of providers:

Cloud Providers:

- Amazon EC2
- Microsoft Azure
- Google Compute Platform

Infrastructure as a Service Providers:

- Red Hat Virtualization
- Red Hat OpenStack Platform
- VMware vSphere
- Microsoft System Center Virtual Machine Manager

Physical Providers:

- Lenovo XClarity

Container Providers:

- OpenShift Container Platform

Let's first verify the providers you have available and check their health status.

### OpenStack Provider status

Let's first check the OpenStack Provider:

1. Navigate to ***Compute*** -> ***Clouds*** -> ***Providers***

    ![navigate to cloud providers](../../common/img/navigate-to-compute-clouds-providers.png)

    :heavy_check_mark: ***NOTE*** Don't click while navigating the main menu structure on the left, just hover until you reach the entry you want...

1. You should see a tile icon labeled "OpenStack". Click on it.

    ![OpenStack provider tile icon](../../common/img/openstack-provider-tile.png)

1. Click on ***Authentication*** -> ***Re-check Authentication Status***

    ![re-check authentication](../../common/img/openstack-recheck-authentication.png)

    This will validate the credentials are correct, and it will also restart the provider specific background processes.

    Click the little arrow to reload the page.

    ![provider page reload](../../common/img/provider-reload.png)

Wait a few moments before you reload the page, the provider tile should show a green check mark and the last refresh fields should report "less than a minute ago" or similar.

:heavy_check_mark: ***NOTE*** Don't worry if the last refresh does not change. As long as the provider icon is showing a green check box, you're good and can carry on with the lab.

:warning: ***WARNING*** If the provider icon does not show a green check mark, consult an instructor before you continue with the lab!

### Red Hat Virtualization Provider status

Let's then check the RHV Provider:

1. Navigate to ***Compute*** -> ***Infrastructure*** -> ***Providers***

    ![navigate to cloud providers](../../common/img/navigate-to-compute-infrastructure-providers.png)

1. You should see a tile icon labeled "RHV". Click on it.

    ![OpenStack provider tile icon](../../common/img/rhv-provider-tile.png)

1. Click on ***Authentication*** -> ***Re-check Authentication Status***

    ![re-check authentication](../../common/img/rhv-recheck-authentication.png)

    This will validate the credentials are correct, and it will also restart the provider specific background processes.

1. Switch to the ***Summary view*** by clicking the little icon on the top right

    ![switch to RHV summary view](../../common/img/rhv-summary-view.png)

1. Click the little arrow to reload the page.

    ![provider page reload](../../common/img/provider-reload.png)

Wait a few moments before you reload the page, the provider tile should show a green check mark and the last refresh fields should report "less than a minute ago" or similar.

:heavy_check_mark: ***NOTE*** Don't worry if the last refresh does not change. As long as the provider icon is showing a green check box, you're good and can carry on with the lab.

:warning: ***WARNING*** If the provider icon does not show a green check mark, consult an instructor before you continue with the lab!

### Red Hat OpenShift Container Platform status

Let's finally check the OpenShift Provider:

1. Navigate to ***Compute*** -> ***Containers*** -> ***Providers***

    ![navigate to container providers](../../common/img/navigate-to-compute-container-providers.png)

1. You should see a tile icon labeled "OpenShift". Click on it.

    ![OpenShift provider tile icon](../../common/img/openshift-provider-tile.png)

1. Click on ***Authentication*** -> ***Re-check Authentication Status***

    ![re-check authentication](../../common/img/openshift-recheck-authentcation.png)

    This will validate the credentials are correct, and it will also restart the provider specific background processes.

1. Click on the little icon ***Summary View*** in the top right

    ![OpenShift provider summary button](../../common/img/navigate-to-openshift-provider-summary-view.png)

1. Check Summary View

    ![OpenShift Provider Summary View](../../common/img/openshift-provider-summary-view.png)

    Click the little arrow to reload the page.

    ![provider page reload](../../common/img/provider-reload.png)

Wait a few moments before you reload the page, the provider tile should show a green check mark and the last refresh fields should report "less than a minute ago" or similar.

:heavy_check_mark: ***NOTE*** Don't worry if the last refresh does not change. As long as the provider icon is showing a green check box, you're good and can carry on with the lab.

:heavy_check_mark: ***NOTE*** Metrics collection has been disabled in this lab. If the "Last Metrics Collection" is not updated, this can be ignored.

:warning: ***WARNING*** If the provider icon does not show a green check mark, consult an instructor before you continue with the lab!

## CloudForms with Ansible batteries included

This first excersie of the lab will guide you through the process of creating a Service Catalog Item based on an Ansible Playbook.

### Introduction to Ansible

Today, every business is a digital business. Technology is your innovation engine, and delivering your applications faster helps you win. Historically, that required a lot of manual effort and complicated coordination. But today, there is Ansible - the simple, yet powerful IT automation engine that thousands of companies are using to drive complexity out of their environments and accelerate DevOps initiatives.

Red Hat CloudForms can integrate with IaaS, PaaS, public and private cloud, and configuration management providers. Since version 4.2 of CloudForms, it can also integrate with Ansible Tower by Red Hat. The latest version which is 4.6, which has an improved "embedded Ansible" role which allows it to run Playbooks, manage credentials and retrieve Playbooks from a source control management like git.

This integration give customers the capability to build Service Catalogs from Ansible Playbooks to allow end users to easily browse, order and manage resources from Ansible. Ansible Playbooks can be used in Control Policies which can not only detect problems, but also automatically fix them. The User Interface of CloudForms can be extended seamless with additional menus and buttons, which utilize Ansible Playbooks to perform user initiated tasks.

### Value provided by a Service Catalog

One of the features a Cloud Management Platform provides, is a Self Service User Interface. From the Service Catalog users can order, manage and retire Services. Services are categorized in Catalogs, where they can be organized and easily consumed.

By providing a Service Catalog, users can deploy the Services they need quickly and easily. This helps to improve agility, reduce provisioning time and free up resources in internal IT.

### Service Basics

But first some basics. Four items are required to make a Service available to users from the CloudForms Self Service Catalog:

1. Provisioning Dialog

   The Provisioning Dialog specifies the list of customizable parameters. For example, when ordering a Virtual Machine, users can specify the number of virtual CPUs, how much memory the VM should have and other parameters. The list of possible parameters is defined in the Provisioning Dialog

1. A Service Dialog

    When the user orders a Service Catalog Item from the Service Catalog, you might want to allow them to override certain default values. For example, you might allow users to choose from a range of values of how much memory the new Virtual Machine can have. You might want them to only choose from a list of predefined values like 2, 4, or 8 GB of RAM - but not more or less. This is specified in the Service Dialog.

1. A Service Catalog Item

    The Service Catalog Item is what users will see in the Service Catalog and are able to order. It usually consists of a Service Dialog allowing users to change specific parameters, it can have a nice icon and an (optional) HTML description. Service Catalog Items are organized in Service Catalogs for easier navigation.

1. A Service Catalog

    The Service Catalog allows administrator to organize the Catalog Items. You might want to have a Catalog for different Virtual Machine types, or one offering certain applications like Wordpress, MariaDB etc. Or you might want to categorize by Operating System. This is done by creating Service Catalogs and adding Items to them.

We can also use Role Based Access Control to make certain Service Catalog Items available only to specific groups of users.

### Power on target VM

The following lab will use UI customizations to illustrate how easy it is to add additional functionality to CloudForms. The example will use an Ansible Playbook which will be executed on a Virtual Machine. Ansible uses SSH to access the remote machine and therefore the VM has to be powered on. The following steps will power on a Virtual Machine which we later use as the target for the Ansible Playbook.

1. Navigate to ***Compute*** -> ***Infrastructure*** -> ***Virtual Machines***

    ![navigate to virtual machines](../../common/img/navigate-to-virtual-machines.png)

1. Tiles represent the Virtual Machines. Note that the VM "cfme001" is powered off.

    ![VM cfme001 is turned off](../../common/img/cfme-001-powered-off.png)

1. Click on the tile icon "cfme001" to see the VM details.

1. Click ***Power*** -> ***Power On*** to power on the Virtual Machine

    ![cfme001 power on ](../../common/img/cfme-001-power-on.png)

1. CloudForms will perform this action in the background and it will take a few minutes to complete. Click on the reload icon in the menu bar to reload the screen.

    ![reload VM details](../../common/img/cfme-001-reload-details.png)

1. Verify the "Power State" of the Virtual Machine has changed to "on" before you proceed with the next steps of the lab.

    ![cfme001 powered on](../../common/img/cfme-001-powered-on.png)

    :heavy_check_mark: ***NOTE*** The VM should also report an IP address in the 192.168.1.0/24 network.

Now our test VM is up and running and we can proceed with the next steps.

### Make sure embedded Ansible role is enabled and running

Before we continue, we want to make sure the embedded Ansible role is enabled and running.

1. Click on your user name on the top right and click on ***Configuration***

    ![navigate to configuration](../../common/img/navigate-to-configuration.png)

1. Make sure the "Embedded Ansible" and the "Git Repositories Owner" Roles are enabled

    ![ansible role enabled](../../common/img/ansible-role-enabled.png)

1. Click on ***Diagnostics*** in the accordion on the left and click on the ***Workers*** tab

1. Make sure you can see a line indicating the "Embedded Ansible Worker" is in state "started"

    :heavy_check_mark: ***NOTE*** The git role is not represented by a specific worker process.

    ![ansible worker started](../../common/img/ansible-worker-started.png)

:warning: ***WARNING*** We've noticed that sometimes the role does not start automatically. You can trigger a restart by clicking on ***Diagnostics*** -> ***Server*** and then ***Configuration*** -> ***Restart Server***. This will trigger a restart of all services and can take a few minutes to complete. Only do this, if your Embedded Ansible role was not in state "started".

![restart CloudForms Server](../../common/img/restart-server.png)

### Add a Git repository of Ansible Playbooks

To be able to run Ansible Playbooks, they have to become available in CloudForms. Custom git repositories can be used as well as GitHub, GitLab or others. Other Source Control Management Systems like Subversion or Mercurial are planned for later versions.

1. Navigate to ***Automation*** -> ***Ansible*** -> ***Repositories***.

    ![navigate to Ansible repositories](../../common/img/navigate-to-ansible-repo.png)

1. Click on ***Configuration*** -> ***Add New Repository***

    ![Add new repository](../../common/img/embedded-ansible-add-git-repository.png)

    :warning: ***WARNING*** If the menu item "Add New Repository" is disabled, the Git Repository Role is not active.

1. Fill in the form.

    An internal name for the git repository:

    ***Name:*** Github

    A description for the git repository:

    ***Description:*** Example Playbooks

    How to access the git repository:

    ***URL:***

        https://github.com/cbolz/summit-fy19.git

    Update on Launch causes CloudForms to check for new Playbooks or updated Playbooks before a Playbook is launched.

    ***SCM Update Options:*** check "Update on Launch"

    ![add a new repository](../../common/img/add-ansible-repository.png)

1. Click on ***Add*** to save the settings

    :heavy_check_mark: ***NOTE*** It takes a few seconds for the action to complete. A pop up notification will inform you after the task was completed.

1. You can click on your username in the top right corner and then on ***Tasks*** to see all currently running tasks. Switch to ***All Tasks*** to see the progress of your Repository import.

1. Verify the task completed successfully

    ![after Ansible repo task compled](../../common/img/task-ansible-repo-import-completed.png)

1. Navigate back to ***Automation*** -> ***Ansible*** -> ***Repositories***.

    ![navigate to Ansible repositories](../../common/img/navigate-to-ansible-repo.png)

1. Click on the ***Reload*** icon to refresh the screen. After the initial import completed, you will see the list of available repositories.

    ![list of Ansible repositories](../../common/img/list-of-ansible-repos.png)

1. Click on the repository to see the details.

    ![Ansible repository details](../../common/img/ansible-repo-details.png)

1. Click on ***Playbooks*** to see the list of automatically imported playbooks.

    ![list of imported playbooks](../../common/img/ansible-list-of-playbooks.png)

This confirms that all playbooks have been imported successfully.

### Store Virtual Machine Credentials

Ansible is using SSH by default to perform actions on the target machine. To be able to login, it has to know the login credentials.

1. Navigate to ***Automation*** -> ***Ansible*** -> ***Credentials***

    ![navigate to Ansible credentials](../../common/img/navigate-to-ansible-credentials.png)

1. Click on ***Configuration*** -> ***Add a new Credential***

    ![add new credentials](../../common/img/ansible-add-credentials.png)

1. Use the following settings:

    A user descriptive name for the Credentials you want to store:

    ***Name:*** Virtual Machine credentials

    CloudForms supports several credential types to connect to other systems. For this lab we chose "Machine":

    ***Credential type:*** Machine

    The username used to login to the target system:

    ***Username:*** root

    The password used to login to the target system:

    ***Password:*** `<to_be_provided>`

    Passwrds are stored encrypted in the CloudForms database.

    ![provide VM credentials](../../common/img/ansible-vm-credentials.png)

1. Click ***Add** to save the credentials

    Once more this is an action which is preformed in the background and it can take a few seconds until you can see the new credentials in the Web UI.

### Create an Ansible Service Catalog

To offer a Service Catalog Item to users, they have to be organized in Service Catalogs. Create one by following these steps:

1. The next step is to create a Service Catalog. First we have to navigate to ***Services*** -> ***Catalogs***.

    ![navigate to services, catalog](../../common/img/navigate-to-service-catalog.png)

1. On this screen click on ***Catalogs*** on the left

    ![service catalogs](../../common/img/service-catalogs.png)

1. Click on ***Configuration*** and ***Add a New Catalog***

1. Fill out name and description:

    A user friendly name of the Service Catalog. End users will see the different Service Catalogs by name:

    ***Name:*** Ansible

    Additional description about the Service Catalog. End users will see the description and it will help them to find the Service Catalog Items they are looking for:

    ***Description:*** Order Ansible Playbooks from a Service Catalog

    ![add a new catalog](../../common/img/add-a-new-catalog-ansible.png)

1. Click on ***Add*** to save the new Catalog

### Create a Service Catalog Item

In the following step we create a Service Catalog Item which will execute an Ansible Playbook.

1. Navigate to ***Services*** -> ***Catalogs***

    ![navigate to Services Catalogs](../../common/img/navigate-to-service-catalog.png)

    :heavy_check_mark: ***NOTE*** If you followed the instructions by the letter, you're already in this part of the UI.

1. Navigate to ***Catalog Items*** in the accordion on the left

    ![navigate to Catalog Items](../../common/img/navigate-to-catalog-items-with-ansible.png)

1. Click on ***Configuration*** -> ***Add a New Catalog Item***

    ![create new catalog item](../../common/img/create-new-catalog-item-with-ansible.png)

1. Select ***Ansible Playbook*** as Catalog Item Type

    ![select ansible playbook as type](../../common/img/ansible-playbook-catalog-item-type.png)

1. Use the following parameters when defining the Service Catalog Item:

    The user friendly name of the Service Catalog Item. It will be presented to the end user:

    ***Name:*** Install Package

    Additional description about the Service Catalog Item to make it easier for the end user to find what they are looking for:

    ***Description:*** Install Package via Ansible Playbook

    You can hide Service Catalog Items from users by setting this to "No". For this lab we want to allow users to order the Service Catalog Item, so we set this to "Yes"

    ***Display in Catalog:*** Yes

    In which Service Catalog do you want the Service Catalog Item to show up?

    ***Catalog:*** Ansible

    You might have many git repositories, to better identify the correct Ansible Playbook, you first select the Repository. We only have one Repository so far, so this is simple:

    ***Repository:*** Github

    The actual Playbook which will be exected when the Service Catalog Item is ordered.

    ***Playbook:*** playbooks/InstallPackage.yml

    The credentials used to login to the target machine to run the Ansible Playbook:

    ***Machine Credentials:*** Virtual Machine credentials

    Ansible Playbooks can use variables which gives us more flexiblity. In this example the package name is not hard coded, but can be set and changed from a variable:

    ***Variables & Default Values***: add one new entry with:

    Since a Playbook can have multiple variables, you can add multiple lines.

    ***Variable:*** package_name

    ***Default Value:*** httpd

    Click the little plus ("+") icon to save the row. We only use one variable in this playbook, but your Playbooks might use more.

    ***Dialog:*** Create New

    Use "InstallPackage" as the name of the Dialog. CloudForms will automatically create the Service Dialog for us, to save some time. The automatically created Service Dialog is still fully customizable, which we will do in a later part of the lab.

    ![dialog to create InstallPackage Service Catalog Item](../../common/img/service-catalog-installpackage.png)

1. Click ***Add*** to save all changes

### Test the Service Catalog Item

We want to make sure the resulting Service Catalog Item actually works.

1. Navigate to ***Services*** -> ***Catalogs***

    ![navigate to service catalogs](../../common/img/navigate-to-service-catalog.png)

1. Click on ***Service Catalogs*** in the accordion on the left, if not already selected

    ![navigate to Ansible Service Catalog](../../common/img/navigate-to-ansible-only-service-catalog.png)

1. Select the "Install Package" Service Catalog Item

    ![select install package Service Catalog Item](../../common/img/select-install-package-item-ansible-only.png)

1. Click ***Order***

1. Select the following options:

    These are the credantials stored in CloudForms earlier, to log into the target machine:

    ***Machine Credentials:*** Virtual Machine Credentials

    On which machine the Playbook should be executed:

    ***Hosts:*** localhost (should already be the default)

    The varaible specified when creating the Service Catalog Item, which can be overriden by the end user during order:

    ***package_name:*** httpd (should already be the default)

    ![parameters for the Ansible InstsallPackage Playboosk](../../common/img/installpackage-order.png)

1. Click on ***Submit***

1. After submitting your order, you will be redirected to the Requests Queue. You should also see pop up notifications on the top right informing you about the progress of your order.

1. :+1: ***OPTIONAL*** Click on ***Refresh*** to monitor the progress of your order

1. Navigate to ***Services*** -> ***My Services***

    ![navigate to My Services](../../common/img/navigate-to-my-services.png)

1. Every time a user places an order a object under "My Services" is created. You should see one tile labeled "Install Package"

    ![My Service Install Package](../../common/img/my-services-installpackage-tile.png)

1. Click on the tile icon to get more details

    ![My Service Install Package Details](../../common/img/my-services-installpackage-details.png)

1. Click on the tab ***Provisioning*** to see details of the Ansible Playbook run

    ![My Service Install Package Provisioning](../../common/img/my-services-installpackage-provisioning.png)

    :heavy_check_mark: ***NOTE*** In this example the Playbook completed successfully. In your case it might be still running and not be complete. Click the little reload icon on the page to reload the information while the Playbook is executed in the background.

This concludes this part of the lab.

## Add a button to a Virtual Machine

CloudForms can easily be extended by adding additional menus and buttons. This allows seamless integration of customizations and making them available to end users.

### Add a Button Group

To add new button to the UI, we first need to create a Button Group. A Button Group is basically a new menu entry in the UI. Buttons and Button Groups can be assigned to several objects in CloudForms.

1. Navigate to ***Automation*** -> ***Automate*** -> ***Customization***

    ![navigate to Customization](../../common/img/navigate-to-customization.png)

1. Click on ***Buttons*** in the accordion on the left

    ![navigate to buttons](../../common/img/navigate-to-buttons.png)

1. Click on ***VM and Instance***

    ![naviate to vm and instance](../../common/img/navigate-vm-ane-instance.png)

1. Click on ***Configuration*** -> ***Add a new Button Group***

1. Enter the following data into the form:

    The name of the Button Group, or menu, as shown in the UI:

    ***Text:*** Tools

    A description text which will be shown when hovering the mouse over the Button Group:

    ***Hover Text:*** Additional tasks

    An icon for the Button Group:

    ***Icon:*** search for the wrench symbol in ***Font Awesome***

    ![pick Wrench symbol](../../common/img/wrench-symbol.png)

    ![tools button group](../../common/img/tools-button-group.png)

1. Click ***Add*** to create the button group

In the next section we will add a button to the group.

### Add a new Button to the Button Group

The previous step created a Button Group, or menu. Now we want add Buttons to the Group:

1. Navigate to ***Automation*** -> ***Automate*** -> ***Customization***

    ![navigate to Customization](../../common/img/navigate-to-customization.png)

    :heavy_check_mark: ***NOTE*** You should already be in this menu if you followed the previous steps

1. Click on the "Tools" Button Group you created in the previous lab

    ![navigate to tools button group](../../common/img/tools-button-group-overview.png)

1. Click on ***Configuration*** -> ***Add a new Button***

    ![add a new button to group](../../common/img/add-new-button-to-group.png)

1. Make the following adjustments:

    There are different Button types to extend the CloudForms UI:

    ***Button Type:*** Ansible Playbook

    Which action should be performed, when a user submits the request. In this example we call the previously created Service Catalog Item, which runs an Ansible Playbook.

    ***Playbook Catalog Item:*** Install Package - this is the Service Catalog Item you created in the previous part of the lab

    On which target system should the Ansible Playbook run? For this lab, we want it to be executed on the selected machine:

    ***Inventory:*** Target Machine

    The name of the Button which will be shown in the UI and should be short and descriptive:

    ***Text:*** Install Package

    A more descriptive text which will be shown if the user hovers the mouse over the Button.

    ***Hover Text:*** Install additional package

    An icon to make the Button easy to find:

    ***Icon:*** Select the Software Package Icon at the "Font Fabulous" tab and click ***Apply***

    ![select software package icon](../../common/img/select-software-package-icon.png)

    ![create Ansible Button](../../common/img/create-ansible-button.png)

1. Click ***Add*** to save the Button

This adds a new Button to the Button Group "Tools".

### Test the Ansible Button Customization

We want to test the resulting customization and see how it works from a user point of view.

1. Navigate to ***Compute*** -> ***Infrastructure*** -> ***Virtual Machines***

    ![navigate to virtual machines](../../common/img/navigate-to-virtual-machines.png)

1. Click on the "cfme001" tile if not already selected

    ![VM cfme001 is turned on](../../common/img/cfme-001-powered-on-ovwerview.png)

1. On the details page of "cfme001" note the new menu "Tools". Click to see the new button "Install Package"

    ![VM with addtional tools menu](../../common/img/cfme-001-tools-button.png)

1. Click on ***Tools*** -> ***Install Package***

    ![Ansible button dialog](../../common/img/ansible-button-dialog.png)

1. We can accept the values and click on ***Submit***

1. Navigate to ***Services*** -> ***My Services***

    ![navigate to Services, My Services](../../common/img/navigate-to-my-services.png)

    :heavy_check_mark: ***NOTE*** You might have to click on ***Active Services*** to see the updated overview of all your services.

1. As a result of your action, a new "My Services" object was created. If you don't see it yet, wait a minute and click on the reload button.

1. Click on the "Install Playbook" item to see the details

    ![details of Ansible Playbook](../../common/img/my-service-ansible-playbook-details.png)

1. Click on the ***Provisioning*** tab to see output from your Ansible Playbook

    ![Ansible Playbook output](../../common/img/my-service-ansible-playbook-output.png)

:heavy_check_mark: ***NOTE*** Ansible is idempotent - this means you can run the same Playbook many times and Ansible detects if the desired state was already reached. In this lab, no changes are necessary, because the package httpd is already installed.

This concludes this part of the Ansible lab.

## Improve the Service Dialog

The automatically generated Service Dialog is not perfect. It might confuse the user with too many input fields. It asks for the "Machine Credentials", but those have already been defined in the Service Catalog Item. It also asks for the "Host", but this one is automatically adjusted to be the selected Virtual Machine. And finally the field "package_name" could benefit from a more descriptive text.

In the following steps, we want to make the Service Dialog more user friendly by simplifying it.

### Edit the Service Dialog

1. Navigate to ***Automation*** -> ***Automate*** -> ***Customization***

    ![navigate to Customization](../../common/img/navigate-to-customization.png)

1. Click on ***Service Dialogs*** in the accordion on the left

    ![navigate to Service Dialogs](../../common/img/service-dialog-accordion-after-ansible-lab.png)

1. Click the check box next to "InstallPackage"

1. Click on ***Configuration*** -> ***Copy the selected Dialog to a new Dialog***

    ![copy install package service dialog](../../common/img/copy-install-package-service-dialog.png)

1. Let's improve the Service Dialog by applying the following changes:

    ***Dialog's name:*** Install Package from Button

1. Hide the element "Machine Credentials" by clicking on the little pen icon.

    ![edit machine credentials](../../common/img/edit-machine-credentials.png)

    :heavy_check_mark: ***NOTE*** The edit icon only shows if you move the mouse pointer over the "Machine Credentials" text box.

    :warning: ***WARNING*** Do not delete the element, only hide it! The element is still needed for some CloudForms internal logic and should not be removed.

1. Click on ***Overridable Options*** and switch the ***Visible*** switch to "No"

    ![visible no for machine credentials](../../common/img/visible-no-for-machine-credentials.png)

1. Click ***Save*** to close the dialog

1. Repeat this for the "Hosts" element. Click on the pen icon next to it.

    ![edit hosts](../../common/img/edit-hosts.png)

    :heavy_check_mark: ***NOTE*** The edit icon only shows if you move the mouse pointer over the "Hosts" text box.

1. Click on ***Options*** and switch ***Visible*** to "No"

    ![visible no for hosts](../../common/img/visible-no-for-hosts.png)

    :warning: ***WARNING*** Do not delete the element, only hide it! The element is still needed for some CloudForms internal logic and should not be removed.

1. Click on the little pen icon next to the "package_name" text box

    :heavy_check_mark: ***NOTE*** The edit icon only shows if you move the mouse pointer over the "package_name" text box.

1. Change the label to something more descriptive:

    ***Label:*** Enter Package Name

    :warning: ***WARINING*** Do not change the field "Name" - it is the name of the variable used internally by CLoudForms and the Ansible Playbook. if you change the name of this field, the Playbook will not pickup the new variable and hence ignore the user input.

1. Also let's give more information to the user by improving the "Help" text:

    ***Help:*** Enter the name of the RPM package to be installed on the system

    ![package_name field details](../../common/img/edit-package_name-field.png)

1. Click ***Save*** to apply the changes

    ![install package Service Dialog](../../common/img/install-package-service-dialog.png)

1. Click ***Save*** To save all changes we made in the Service Dialog

This concludes this part of the lab.

### Create improved Service Catalog Item

To be able to use the new Service Dialog with our button, we first have to create an additional Service Catalog Item, which points to the Service Dialog.

1. Navigate to ***Services*** -> ***Catalogs***

    ![navigate to Services Catalogs](../../common/img/navigate-to-service-catalog.png)

1. Navigate to ***Catalog Items*** in the accordion on the left

    ![navigate to Catalog Items](../../common/img/navigate-to-catalog-items-with-ansible-and-install-package.png)

1. Click on ***Configuration*** -> ***Add a New Catalog Item***

    ![create new catalog item](../../common/img/create-new-catalog-item-with-ansible-and-install-package.png)

1. Select ***Ansible Playbook*** as Catalog Item Type

    ![select ansible playbook as type](../../common/img/ansible-playbook-catalog-item-type.png)

1. Use the following parameters when defining the Service Catalog Item:

    ***Name:*** Install Package from Button

    ***Description:*** Install Package via Ansible Playbook

    ***Display in Catalog:*** Yes

    ***Catalog:*** Ansible

    ***Repository:*** Github

    ***Playbook:*** playbooks/InstallPackage.yml

    ***Machine Credentials:*** Virtual Machine credentials

    ***Variables & Default Values***: add one new entry with:

    ***Variable:*** package_name

    ***Default Value:*** httpd

    :heavy_check_mark: ***NOTE*** Click the little plus ("+") icon to save the row.

    ***Dialog:*** Use Exiting

    Use "Install Package from Button" as the name of the Dialog, which is the one we created in the step before.

    ![dialog to create InstallPackage Service Catalog Item](../../common/img/service-catalog-installpackage-from-button.png)

1. Click ***Add*** to save all changes

### Update the Button definition

As the last step, we have to change the definition of our button, to point to the just created Service Catalog Item.

1. Navigate to ***Automation*** -> ***Automate*** -> ***Customization***

    ![navigate to Customization](../../common/img/navigate-to-customization.png)

1. Click on ***Buttons*** in the accordion on the left

    ![navigate to buttons](../../common/img/navigate-to-buttons.png)

1. Click on the "Install Package" Button you created in the previous lab

    ![navigate to tools button group](../../common/img/install-package-button-overview.png)

1. Click on ***Configuration*** -> ***Edit this Button***

1. Change the Playbook Catalog item to the new one you just created "Install Package from Button"

    ![change playbook catalog item](../../common/img/button-change-playbook-catalog-item.png)

1. Click ***Save*** to store all changes

### Test the improved Button

1. Navigate to ***Compute*** -> ***Infrastructure*** -> ***Virtual Machines***

    ![navigate to virtual machines](../../common/img/navigate-to-virtual-machines.png)

1. Click on the "cfme001" tile if not already selected

    ![VM cfme001 is turned on](../../common/img/cfme-001-powered-on-ovwerview.png)

1. On the details page of "cfme001" click on ***Tools*** -> ***Install Package***

    ![VM with addtional tools menu](../../common/img/cfme-001-tools-button.png)

1. Click on ***Tools*** -> ***Install Package***

    ![Ansible button dialog](../../common/img/ansible-button-improved-dialog.png)

    You should see the simplified version of the Dialog. The Package Name has a better description, there is a tool tip if you hover the mouse over the little "i" icon and the redundant fields for "Machine Credentials" and "Hosts" are gone.

1. Click ***Submit*** to execute the Button action

1. Navigate to ***Services*** -> ***My Services***

    ![navigate to Services, My Services](../../common/img/navigate-to-my-services.png)

1. As a result of your action, a new "My Services" object was created. If you don't see it yet, wait a minute and click on the reload button.

1. Click on the "Install Playbook" item to see the details

    ![details of Ansible Playbook](../../common/img/my-service-ansible-playbook-details-with-updated-button.png)

1. Click on the ***Provisioning*** tab to see output from your Ansible Playbook

    ![Ansible Playbook output](../../common/img/my-service-ansible-playbook-output-without-change.png)

This concludes this part of the Ansible lab.

:+1: ***OPTIONAL*** Feel free to repeat this part of the lab with a different package name. You could use "screen" as an example instead of httpd - or some other package you want to install.

## Build a Service Catalog to create and delete users

In this lab we will use an Ansible Playbook to create a local user in CloudForms. This example will also demonstrate how we can define a retirement process as well. In CloudForms' understanding of complete life cycle management, every object should have a provisioning and a retirement workflow.

### Create a Service Catalog Item for the Playbook

1. Navigate to ***Services*** -> ***Catalogs***

    ![navigate to Services Catalogs](../../common/img/navigate-to-service-catalog.png)

1. Click on ***Catalog Items*** in the accordion on the left

    ![navigate to service catalog items](../../common/img/add-catalog-item.png)

1. Click on ***Configuration*** -> ***Add a New Catalog Item***

1. Select ***Ansible Playbook*** as "Catalog Item Type"

    ![add catalog item ansible Playbook](../../common/img/ansible-playbook-catalog-item-type.png)

1. Fill out the form to define the service catalog item:

    ***Name:*** Create User

    ***Description:*** Order this catalog item to create a new user

    ***Display in Catalog:*** Yes (check the box)

    ***Catalog:*** Ansible

    ***Repository:*** Github

    ***Playbook:*** playbooks/SimpleExample/create-user.yml

    ***Machine Credentials:*** CFME Default Credentials

    In the box ***Variables & Default Values*** we can enter the variables the Playbook requires:

    ***Variable:*** create_user_name

    ***Default:*** example

    Click on the little plus icon (+) to save the variable. Repeat the process for the second variable:

    ***Variable:*** create_user_password

    ***Default:*** secret

    Click on the little plus icon (+) to save the variable.

    ***Dialog:*** create new

    ***Dialog name:*** create-user

    ![create user service dialog](../../common/img/create-new-user-prov.png)

1. Click on the tab ***Retirement*** to switch to the second page of the form.

    ***Repository:*** Github

    ***Playbook:*** playbooks/SimpleExample/delete-user.yml

    ***Machine Credentials:*** CFME Default Credentials

    There are no variables needed for retirement and the ***Variables & Default Values*** can be left empty.

    ![create user service dialog retirement](../../common/img/create-new-user-retire.png)

1. Click on ***Add*** to save the catalog item

### Order the "create user" Service Catalog Item

To make sure everything works as expected, we want to test the Catalog Item we just created.

1. Navigate to the Service Catalog by clicking on ***Services*** -> ***Catalogs***

    ![navigate to service catalog](../../common/img/navigate-to-service-catalog.png)

    :heavy_check_mark: ***NOTE*** If you followed the instructions by the letter, you're already in this part of the UI.

1. Click on ***Service Catalog*** in the accordion on the left

1. Click on the Catalog Item you just created:

    ![navigate to service catalog](../../common/img/service-catalog-overview-create-user.png)

1. Click ***Order***

1. The default values in the form can be left alone. Optionally you can specify a different user name and password

    ![create user order form](../../common/img/create-user-order-form.png)

1. Click ***Submit***

    After clicking "Submit" you will be redirected to the Request Queue.

    ![request queue after ordering create user](../../common/img/request-queue-create-user.png)

### Monitor create user Playbook execution

When executing an Ansible Playbook with the embedded role in CloudForms, a "Service" object is automatically created. This service object gives us more details about the executed Playbook. It provides the output of the Playbook and it allows us to trigger retirement.

1. Navigate to ***Services*** -> ***My Services***

    ![navigate to my services](../../common/img/navigate-to-my-services.png)

1. You should see a new tile representing the Ansible Playbook Service you just ordered

    :heavy_check_mark: ***NOTE*** If you don't see the tile yet, wait a minute and try again.

    ![create user service tile](../../common/img/my-service-create-user-tile.png)

1. After clicking on the icon, we can see more details about the service which was created

    ![create user service details](../../common/img/create-user-service-details.png)

    Since this Service does not create a Virtual Machine, the box "VMs" will always say "No Records found"

1. Click on the ***Provisioning*** tab to see the output of the Ansible Playbook

    ![ansible Playbook output](../../common/img/ansible-playbook-output.png)

    If the Playbook execution has not completed, you can click the reload icon to refresh the information. The ***Reload*** icon is represented by a little arrow, left of the ***Configuration*** menu.

    ![reload icon](../../common/img/reload-icon.png)

    :heavy_check_mark: ***NOTE*** If the Playbook execution has not started yet, you might not see any details in the "Provisioning" tab. Wait a minute and reload once more.

### Verify Playbook results

To make sure the user was really created, follow these steps.

1. Click on your username on the top right and click on ***Configuration***

    ![navigate to configuration](../../common/img/navigate-to-configuration.png)

1. Click on ***Access Control*** in the accordion on the left

    ![navigate to access control](../../common/img/access-control.png)

1. Click on ***Users*** and you should see the user you just created (in this screenshot the user is called "example")

    ![user example exists](../../common/img/user-example.png)

1. :+1: ***OPTIONAL*** If you want, you can log out of CloudForms and try to log in with the user you just created. Click on your username on the top right and ***Logout***.

    ![logout](../../common/img/logout.png)

## Advanced labs

If you were able to complete all the steps and still have some time left, here are a couple of things you can do to get more familiar with CloudForms.

### Use the Self Service user Interface

The user interface we used so far is often referenced as the "Operations UI" or the "Classic UI". A new, more modern, Self Service user Interface is also available and receives improvements with every release.

The Self Service user Interface can be accessed by appending the string "self_service" to the Appliance URL.

    https://cf46-<GUID>.labs.rhepds.com/self_service

You can login with the same credentials as before.

### Build a button to execute remote commands

You have learned how to create a Service Dialog, Ansible Playbook Service Catalog Item and how to use them from a Button to extend the out of the box features provided by CloudForms. We can use this knowledge to implement a button to allow users to execute remote commands on a Virtual Machine.

This is a very popular use case because it provides a number of advantages:

- administrators can allow VM owners to run specific commands themselves, so they don't have to open a service request with IT
- administrators can also use CloudForms' powerful Role Based Access Control to make buttons only available to specific user groups
- administrators can grant end users to run commands as a privileged user (e.g. root), without handing out credentials or setting up ACL's on all managed systems
- users can run specific tasks by themselves and don't have to open an internal ticket or wait for someone with the necessary privileges to do it for them

Since this is an advanced lab, there are no detailed step by step instructions. Instead here are couple of pointers to get you on track:

#### The use case

We want end users to able to run certain remote commands by themselves. First we try this with a text box where users can enter their command - but as an additional improvement you should try to replace the text box with a drop down list, where users can only select from a list of pre approved commands.

#### Service Dialog

Based on your work with "Install Package" Service Dialog, you should know what is needed to create a new Service Dialog for this use case.

Start with a simple copy of your working example. Add a text box to ask the user for the command. It is important that you set the name for the text element correctly.

:warning: ***WARNING*** Make sure the text box name is called "param_command" - because "command" is the name of the extra variable in the Ansible Playbook. If you chose a different name, the Playbook will use the default command, which is "echo hello world".

#### Service Catalog Item

To be able to call an Ansible Playbook from a button, you need to create a Service Catalog Item first. This should be very easy for you, since you've done this before in this lab. Just make sure you run the correct playbook and use the Service Dialog you created in the previous step.

The name of the Ansible Playbook is "operatorcommand.yaml"

#### Button

Create a new Button and add it to the existing Button Group "Tools" - or create a new one. Use the Service Catalog Item created in the previous step when you define the button.

#### Improve it further

The advanced settings of a Button allow you to use Role Based Access Control. Check the "Role Access" option at the bottom of the settings page.

Another cool feature is the "Enablement". Since we are using Ansible Playbooks, the Virtual Machine has to be powered on, or the Playbook will fail. With the "Enablement" you can disable your button, if the VM is off and show a pop up notification explaining the situation to the user.

You can use the expression builder to check if the field "VM and Instance: Power State" has the value "on". Use the "Disabled Button Text" to show a hint to the user, for example:

    The VM has to be powered on to execute this action

And if you're still having more time, you can use the "Visibility" to show the Button only for Linux VMs, and not for Windows.

#### Need Help?

Don't hesitate to ask any of the lab organizers for help, if you're stuck!

## Even more?

If you're already done and still have some time left, here are some ideas for advanced labs:

- try to retire the "create user" service catalog item and see if the user is indeed deleted
- upload icons to make the Service Catalog more appealing
