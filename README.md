# One-click deploy your own person hubot with slack integration to Azure

## Introduction

This project allows you to deploy your own personalal [hubot](https://hubot.github.com/) to azure with slack  integration already configured. The 'Deploy to Azure will create a web App to host hubot and a storage account where hubot's brain will be persisted. 

## Instructions

Its important that your **fork** this repository before clicking the 'Deploy to Azure' button, so that the web app is linked to your repository and you can add additional hubot scripts.

Once you have fork this repository, click the 'Deploy to Azure' button below

<a href="https://azuredeploy.net/" target="_blank">
    <img src="http://azuredeploy.net/deploybutton.png"/>
</a>

Below are the parameters that the template expects

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>hostingPlanName</td>
            <td>string</td>
            <td>The name of the app service plan to use for hosting the web app</td>
        </tr>
        <tr>
            <td>location</td>
            <td>string</td>
            <td>
                The location to use for creating the web app, hosting plan and storage account<br/>
                NOTE: Unfortunately the latest version of storage accounts are not avaliable in the Australian data centres yet.
                <ul>
                    <li>Central US</li>
                    <li>East Asia</li>
                    <li>East US</li>
                    <li>East US 2</li>
                    <li>Japan East</li>
                    <li>Japan West</li>
                    <li>North Central US</li>
                    <li>North Europe</li>
                    <li>South Central US</li>
                    <li>Southeast Asia</li>
                    <li>West Europe</li>
                    <li>West US</li>
                </ul> 
				<br/><br/
				
            </td>
        </tr>
        <tr>
            <td>sku </td>
            <td>string</td>
            <td>
				The pricing tier for the hosting plan
	            <ul>
	                <li>Free</li>
	                <li>Shared</li>
	                <li>Basic</li>
	                <li>Standard</li>
	            </ul>
			</td>
        </tr>
        <tr>
            <td>workerSize</td>
            <td>string</td>
            <td>
				The instance size of the hosting plan
	            <ul>
	                <li>Small</li>
	                <li>Medium</li>
	                <li>Large</li>
	            </ul>
			</td>
        </tr>
        <tr>
            <td>enableAlwaysOn</td>
            <td>string</td>
            <td>
				Enable or disable always on. If you choose free or shared for the sku, this should be set to false as it is not supported
				<ul>
					<li>True</li>
					<li>False</li>
				</ul>
			</td>
        </tr>
        <tr>
            <td>storageAccountName</td>
            <td>string</td>
            <td>The name of the storage account that will host hubot's brain</td>
        </tr>
        <tr>
            <td>storageAccountType</td>
            <td>string</td>
            <td>
				The type of storage account
				<ul>
					<li>Standard_LRS = Locally-redundant storage</li>
					<li>Standard_GRS = Geo-redundant storage</li>
					<li>Standard_ZRS = Zone-redundant storage</li>
				</ul>
			</td>
        </tr>
        <tr>
            <td>slackApiToken</td>
            <td>string</td>
            <td>The hubot API token from Slack. <br/><br/>To configure hubot integration go to [your-slack].slack.com/new/hubot, give your hubot a name, click 'Add hubot integration and enter the generated API Token here.</td>
        </tr>
    </tbody>
</table>

## Usage

NOTE: `<name-of-your-hubot>` is the hubot name you configured in the slack integration

Once deployment is complete, you should be able to access `https://<name-of-your-site>.azurewebsites.net/<name-of-your-hubot>/help` and see the list of commands available in Hubot.

In you slack channel you should also be able to `<name-of-your-hubot> help` to also see the list of available commands (for example `hutbot help`)

## Adding additonal hubot scripts

See https://hubot.github.com/docs/#scripts for instructions on adding additional script. 

Unfortunately [Slingshot](https://github.com/projectkudu/slingshot) (the project that implements the Deploy To Azure button) does not currently support continuous deployment (see [https://github.com/projectkudu/slingshot/issues/21](https://github.com/projectkudu/slingshot/issues/21)). This means that changes to your repository are not automatically deployed. 

Instead, once you have pushed your changes to your repository, you have to manually sync via the portal. If you go the web app blade, you will see a 'deployment' tile. Clicking on this will bring up a new blade with a 'Sync' button. Clicking on the 'Sync' button will pull the latest changes from your repository. When complete, click 'Restart' to restart your web app to see the new scripts.
