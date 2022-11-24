# This is a work in progress! Please do not use for any production workloads *yet*.


# sled-ttl
Sled TTL is a TTL plugin for https://github.com/spacejam/sled and https://github.com/komora-io/concurrent-map

## Goals
1. Reliability
2. Performance
3. Ease of use

In that order

## **TTL methodology?**
There's two ways to approach TTL for k/v objects:

### 1. Check TTL as the object is called
- Uses https://github.com/komora-io/concurrent-map - a lock free B+ in-mem map that has high-performance
- This option has obvious performance benefits, however it does mean stale objects can linger in the DB if they've never been called.
- TTL can be edited if the object is called again (there will have to be a safety if TTL is called, but by the time it is changed, the object has expired), however if the object is called again or assigned a new value the TTL will remain the same.
- This will be better for use cases where you can afford stale entries, such as ratelimiting.

### 2. Check TTL in the background
- Uses https://github.com/spacejam/sled - embedded lock-free k/v db with optional zstd compression
- Ranges over the Sled IVec protected by the Arc in a different thread
- Check the TTL in a different thread and purge expired entries
- This option is better when you can't afford to have stale entries (such as caching)

## Usage
Coming soon!
