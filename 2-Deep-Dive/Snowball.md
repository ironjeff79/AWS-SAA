# Snowball
- It is a physical data transport solution which helps moving terra bytes or peta bytes of data in our out of AWS
- Alternative to move data over network (in case of huge amount of data)
- It is secure, temper resistant, it uses KMS 256 bit encryption
- It has tracking using SNS and text messages. It has an E-ink shipping label
- Uses pay for data transfer jobs
- Use cases: large data cloud migrations, DC decommissions, disaster recovery
- If it takes more than a week to transfer over the network the data, it probably would be recommended to use a Snowball device

## Snowball Process
- Request a snowball device from AWS console for delivery
- Install the snowball client on the local server
- Connect the snowball device to the server and copy the files over using the client
- Shipt back the device when the all the necessary data is transferred to the device
- The data from the Snowball will be loaded into an S3 bucket
- Snowball is completely wiped

## Snowball Edge
- Snowball Edge adds computational capability to the device
- It can have 100TB of capacity with either:
    - 24 vCPU (Storage optimized)
    - 52 vCPU & optional GPU (Compute optimized)
- Supports a custom EC2 AMI so it can perform processing on the go
- Supports custom Lambda functions
- It is useful for pre-processing data while it is moving
- Use cases: data migration, image collation, IoT capture, machine learning

## Snowmobile
- It is truck which can transfer exabytes of data
- Each Snowmobile has 100PT of data storage capacity
- Better than Snowball if more than 10PB of data should be transferred

## Snowball into Glacier
- Snowball can not import data directly to Glacier
- We have to use Amazon S3 first, adn an S3 lifecycle policy

# Snowball Cheatsheet
**LOW COST** It cost thousands of dollars to transfer 100TB over high speed internet.Snowball can reduce that costs by **1/5th**


**SPEED** It can take 100TB over 100 days to transfer over high speed internet. 
Snowball can reduce that transfer time by **less than a week**

**SNOWBALL FEATURES AND LINITATIONS** 
- E-Ink display(shipping information)
- Tamper and weather proof 
- Data is encrypted end-to-end (256-bit encryption)
- uses Trusted Platform Moudle(TPM)
- For security purposes,data transfers must be completed within **90 days** of the Snowball being prepared.
- Snowball can **Import** and **Export** from **S3** 

**Snowballs comes in two sizes**
- **50TB**(42TB of usable space)
- **80TB**(72TB of usable space)

# Snowball Edge Cheatsheet
Similar to Snowball but with **more storage** and with **local processing**

**Snowball Edge features and limitations**
- LCD display(shipping information and other functionality)
- can undertake local processing and edge-computing workloads
- Can use in a cluster in groups of 5 to 10 devices 
- three options for device configurations 
    - storage optimized (24 vCPUs)
    - compute optimized (54 vCPUs)
    - GPU optimized (54 vCPUs)

**Snowball Edge comes in two sizes**
- **100TB**(83TB of usable space)
- **100TB Clustered**(45TB per node)

# Snowball & Snowball Edge & Snowmobile Cheatsheet
- **Snowball** and **Snowball Edge** is a rugged container which contains a storage device
- **Snowmobile** is a 45-foot long ruggedized shipping container,pulled by a semi-trailer truck.
- Snowball and Snowball Edge is for **peta-scale** migration.Snowball is for **exabyte-scale** migration.
- **LOW COST** thousands of dollars to transfer 100TB over high speed internet.Snowball is **1/5th**  
- **SPEED** 100TB over 100 days to transfer over high speed internet, Snowball takes **less than a week**

**Snowballs comes in two sizes**
- **50TB**(42TB of usable space)
- **80TB**(72TB of usable space)

**Snowball Edge comes in two sizes**
- **100TB**(83TB of usable space)
- **100TB Clustered**(45TB per node)

**Snowmobile comes in one size** 100PB
- You can both **export** or **import** data using Snowball or Snowmobile 
- You can import into **S3** or **Glacier**
- **Snowball Edge** can undertake local processing and edge-computing workloads
- **Snowball Edge** can use in a cluster in groups of 5 to 10 devices
- **Snowball Edge** provides three options for devices configutations

