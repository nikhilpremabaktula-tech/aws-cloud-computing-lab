Experiment 10: Manage Persistent Storage Using Amazon EBS

Aim

To study the creation, attachment, configuration, snapshot, and restoration of Amazon Elastic Block Store (EBS) volumes for persistent storage with EC2 instances.

Requirements

- AWS account or access to an AWS lab (not used in this documentation-only exercise)
- Amazon EC2 and EBS
- Basic Linux commands

Task 1: Create a New EBS Volume

1. Open AWS Console and navigate to EC2 → Volumes.
2. Select Create volume.
3. Choose General Purpose SSD (gp3 or gp2, as available).
4. Set size to 1 GiB.
5. Select the Availability Zone used by the EC2 instance.
6. Add the tag Name = My Volume.

Task 2: Attach the Volume

1. Select My Volume.
2. Choose Actions → Attach volume.
3. Select the EC2 instance.
4. Attach the volume.

Task 3: Connect to EC2

1. Navigate to EC2 → Instances.
2. Select the running instance.
3. Choose Connect → EC2 Instance Connect.

Task 4: Configure the File System

Example commands for an appropriately configured Linux EC2 instance:

lsblk
df -h
sudo mkdir -p /mnt/data-store

After identifying the new, empty EBS device, create a filesystem and mount it. Replace /dev/DEVICE with the verified device path.

sudo mkfs -t ext4 /dev/DEVICE
sudo mount /dev/DEVICE /mnt/data-store
echo "some text" | sudo tee /mnt/data-store/file.txt
cat /mnt/data-store/file.txt

Safety: Never format the root disk or an existing disk containing important data.

Task 5: Create an EBS Snapshot

1. Open EC2 → Volumes.
2. Select My Volume → Actions → Create snapshot.
3. Add the tag Name = My Snapshot.
4. Wait for the snapshot status to become Completed.
5. Delete the test file to prepare for a recovery test.

Task 6: Restore the Snapshot

1. Select the completed snapshot.
2. Choose Create volume from snapshot.
3. Select the EC2 instance's Availability Zone.
4. Attach the restored volume.
5. Identify the restored device using lsblk.
6. Mount its existing filesystem at a different directory and check whether file.txt is present.

Expected Result

The EBS volume should be created, attached, and mounted. A snapshot should preserve the test file so it can be recovered after deletion.

Actual Result

Not executed. AWS access was unavailable during this documentation-only exercise.

Conclusion

Amazon EBS provides persistent block storage for EC2 instances. EBS snapshots support backup and recovery of stored data.

Evidence

Add screenshots when the experiment is performed in an AWS lab.
