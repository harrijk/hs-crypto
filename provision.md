---

copyright:
  years: 2018, 2020
lastupdated: "2020-07-02"

keywords: provision, crypto unit, service instance, create service instance, kms service instance, cloud hsm service instance, hpcs cli

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}
{:tip: .tip}
{:important: .important}
{:external: target="_blank" .external}
{:term: .term}

# Provisioning service instances
{: #provision}

You can create an instance of {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} by using the {{site.data.keyword.cloud_notm}} console or the {{site.data.keyword.cloud_notm}} CLI.
{: shortdesc}

## Before you begin
{: #provision-prerequisites}

In order to provision a {{site.data.keyword.hscrypto}} instance, make sure that you have a [Pay-As-You-Go or Subscription {{site.data.keyword.cloud_notm}} account](/docs/account?topic=account-accounts).

1. To check your account type, go to [{{site.data.keyword.Bluemix_notm}}](https://cloud.ibm.com/login){: external} and click **Management** > **Account** > **Account settings**.

2. If you have a Lite account and want to use {{site.data.keyword.hscrypto}}, [upgrade your account to a Pay-As-You-Go or Subscription account](/docs/account?topic=account-upgrading-account). You can also [apply your promo code](/docs/billing-usage?topic=billing-usage-applying-promo-codes) if you have one.

## Provisioning from the {{site.data.keyword.cloud_notm}} console
{: #provision-gui}

To provision an instance of {{site.data.keyword.hscrypto}} from the {{site.data.keyword.cloud_notm}} console, complete the following steps:

1. [Log in to your {{site.data.keyword.cloud_notm}} account](https://cloud.ibm.com/login){: external}.
2. Click **Catalog** to view the list of services that are available on {{site.data.keyword.cloud_notm}}.
3. From the Catalog navigation pane, click **Services**. And then, under **Category**, select **Security**.
4. From the list of services displayed, click the **{{site.data.keyword.hscrypto}}** tile.
5. Fill in the form with the details that are required.
  1. Select a [region](/docs/hs-crypto?topic=hs-crypto-regions) that you want to create your {{site.data.keyword.hscrypto}} resources in.
  2. **Optional**: In the **Tags** field, add tags to organize your resources. If your tags are billing related, consider writing tags as `key: value` pairs to help group-related tags, such as `costctr:124`. For more information about tags, see [Working with tags](/docs/account?topic=account-tag).
  3. Under **Number of crypto units**, select the number of [crypto units](#x9860404){: term} that meets your performance needs.

    In a production environment, it is suggested to select at least two crypto units to enable high availability. If you select three or more crypto units, these crypto units are distributed among different supported availability zones in the selected region.
    {: important}
6. Click **Create** to provision an instance of {{site.data.keyword.hscrypto}} in the account, region, and resource group where you are logged in.

## Provisioning from the {{site.data.keyword.cloud_notm}} CLI
{: #provision-cli}

To provision an instance of {{site.data.keyword.hscrypto}} with the {{site.data.keyword.cloud_notm}} CLI, complete the following steps:

1. Download and install the [{{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-getting-started){: external}.

2. Log in to {{site.data.keyword.cloud_notm}} through the {{site.data.keyword.cloud_notm}} CLI with the following command:

    ```sh
    ibmcloud login
    ```
    {: pre}

    If the login fails, run the `ibmcloud login --sso` command to try again. The `--sso` parameter is required when you log in with a federated ID. If this option is used, go to the link listed in the CLI output to generate a one-time passcode.
    {: tip}

3. Select the region and resource group where you would like to create a {{site.data.keyword.hscrypto}} service instance. You can use the following command to set your target region and resource group.

    ```sh
    ibmcloud target -r <region_name> -g <resource_group_name>
    ```
    {: pre}

    Replace the variables in the sample command according to the following table.

    <table>
      <tr>
        <th>Variables</th>
        <th>Description</th>
      </tr>
      <tr>
        <td>*region_name*</td>
        <td>The region abbreviation, such as `us-south` or `au-syd`, that represents the geographic area where your {{site.data.keyword.hscrypto}} service instance resides. For more information, see [Regional service endpoints](/docs/hs-crypto?topic=hs-crypto-regions).</td>
      </tr>
      <tr>
        <td>*resource_group_name*</td>
        <td>The resource group where you organize and manage the instance. You can select the initial resource group that is named `Default` or other groups that you create. For more information, see [Creating and managing resource groups](/docs/account?topic=account-rgs).</td>
      </tr>
      <caption style="caption-side:bottom;">Table1. Describes command variables to set the target region and resource group</caption>
    </table>

4. Run the following command to create a {{site.data.keyword.hscrypto}} instance:

    ```sh
    ibmcloud resource service-instance-create <instance_name> hs-crypto standard <region_name> [-p '{"units": <number_of_crypto_units>}']
    ```
    {: pre}

    Replace the variables in the example command according to the following table.

    <table>
      <tr>
        <th>Variables</th>
        <th>Description</th>
      </tr>
      <tr>
        <td>*instance_name*</td>
        <td>Mandatory. The name of your {{site.data.keyword.hscrypto}} service instance.</td>
      </tr>
      <tr>
        <td>*region_name*</td>
        <td>Mandatory. The region abbreviation, such as `us-south` or `au-syd`, that represents the geographic area where your {{site.data.keyword.hscrypto}} service instance resides. For more information, see [Regional service endpoints](/docs/hs-crypto?topic=hs-crypto-regions).</td>
      </tr>
      <tr>
        <td>*number_of_crypto_units*</td>
        <td>Optional. Multiple crypto units are distributed among different supported availability zones in the selected region to increase availability. You can specify 1 to 3 crypto units. In a production environment, it is suggested to select at least two crypto units to enable high availability. If you do not specify the number of crypto units, two crypto units are assigned by default.</td>
      </tr>
      <caption style="caption-side:bottom;">Table2. Describes command variables to create a {{site.data.keyword.hscrypto}} service instance</caption>
    </table>

5. Verify that the service instance is created successfully. Run the following command to get all the service instances you create. Check whether the {{site.data.keyword.hscrypto}} service instance is among the list.

    ```sh
    ibmcloud resource service-instances
    ```
    {: pre}


## What's next
{: #provision-next}

* Initialize your service instance with the [{{site.data.keyword.IBM_notm}} {{site.data.keyword.hscrypto}} Management Utilities](/docs/hs-crypto?topic=hs-crypto-initialize-hsm-management-utilities) or the [{{site.data.keyword.cloud_notm}} TKE CLI plug-in](/docs/hs-crypto?topic=hs-crypto-initialize-hsm) so that {{site.data.keyword.hscrypto}} can provide key management and data management functions.
* To find out more about programmatically managing your keys, check out the [{{site.data.keyword.hscrypto}} key management API reference doc](https://{DomainName}/apidocs/hs-crypto){: external}.
* To find out more about encrypting your data by using the cloud HSM function of {{site.data.keyword.hscrypto}}, check out the [PKCS #11 API reference](/docs/hs-crypto?topic=hs-crypto-pkcs11-api-ref) and [GREP11 API reference doc](/docs/hs-crypto?topic=hs-crypto-grep11-api-ref).
* If you need to delete your service instance, refer to [Deleting service instances](/docs/hs-crypto?topic=hs-crypto-delete-instance) for instructions.
