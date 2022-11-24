# This is a work in progress! Please do not use for any production workloads *yet*.


# sled-ttl
Sled TTL is a TTL plugin for https://github.com/spacejam/sled

## Goals
1. Reliability
2. Performance
3. Ease of use

In that order

## **TTL methodology?**
There's two ways to approach TTL for k/v objects:

### 1. Check TTL as the object is called
- This option has obvious performance benefits, however it does mean stale objects can linger in the DB if they've never been called.
- TTL can be edited if the object is called again (there will have to be a safety if TTL is called, but by the time it is changed, the object has expired), however if the object is called again or assigned a new value the TTL will remain the same.
- This will likely be better for use cases where you can afford stale entries, such as ratelimiting.

### 2. Check TTL in the background 
- Ranges over the Sled IVec protected by the Arc in a different thread
- This option is better when you can't afford to have stale entries (such as caching)
- Check the TTL in a different thread and purge expired entries
- This probably will not be able to used in conjuction with checking the TTL as the object is called, however, it could be in the future

## Usage
Coming soon!
