# Corrupted Shuffle Blocks

Corrupted Shuffle Blocks are generally rare and most commonly indicate a hardware level problem. If you see a lot of `Block shuffle_[somenumbershere] is corrupted but the cause is unknown` the next step is to see if they're all coming from the same host. You can do this by grepping the driver stderr log for `FetchFailed(BlockManagerId(` and if the hostname of the block manger is the same (note: there may be different block manager ids) then that host is likely the problematic host.


For example in `24/09/25 00:21:37 WARN task-result-getter-0 TaskSetManager: Lost task 613.0 in stage 1.0 (TID 12901) (fetching-host-name.internal executor 42): FetchFailed(BlockManagerId(420, serving-host-name.internal, 7337, None), shuffleId=0, mapIndex=11187, mapId=11187, reduceId=613, message=` the host we are concerned about is the `serving-host-name.internal`. At this point you'll need to work with your cluster administrator to remove that host. If you're running on EC2 (or another cloud) you may also need to create a ticket with upstream so that the node (once removed) is not added back from auto-scaling.


