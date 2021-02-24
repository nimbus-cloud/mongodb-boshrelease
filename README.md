Before creating release please download mongodb-3.6.22.tgz from https://fastdl.mongodb.org/linux/mongodb-linux-x86_64-ubuntu1604-3.6.22.tgz and place it in to /src/mongod directory.

Below should be run done only on brand new deployment.

To bootstrap replica set and create an admin user:

1. Pick a non-arbiter node after all nodes are deployed
2. Ssh into that node
3. Bootstrap replica set:
 
    export PATH=$PATH:/var/vcap/packages/mongod/
    mongo /var/vcap/jobs/mongod/bootstrap/replica_set.js

4. Wait for a while for the replica set to initiate, the node on which bootstrap was done will become primary after few seconds
5. Create admin user: 

    mongo /var/vcap/jobs/mongod/bootstrap/create_admin_user.js

Currently I cannot think of a way of automating this, hence these two scripts has to be run manually.

Automation is problematic because:
1. These two scripts should be run when all vms have been deployed. See (1)
2. Because we have a replica set name in the config, it is not possible to create admin user before replica set is bootstrapped.