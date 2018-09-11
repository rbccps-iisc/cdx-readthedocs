CDX Users
=========

The CDX mainly consist of 3 types of users:

#. **Human users (or owners)** : who own devices and apps that are to be connected with the CDX.
#. **Subscribers** : The devices or apps whose main purpose to connect with the CDX is to subscribe for data.
#. **Publishers** : The devices or apps whose main purpose to connect with the CDX is to publish data.

Each owner after successful registration with the CDX is provided with:

#. **Owner’s follow bus created at the CDX** : The purpose of this bus is to allow other users to request for accessing owner’s devices/apps. Thus, this bus is writable by all valid users.

#. **Owner’s follow queue created at the CDX** : This queue allows the owner to get the follow requests mentioned above. This queue can only be controlled by the owner.

Each subscriber after successful registration with CDX is provided with:

#. **Subscriber’s queue** : This queue provides the subscriber with the messages from devices/apps which the subscriber has subscribed to. This queue can only be controlled by the owner of the subscriber.
#. **Subscriber’s priority queue** : This queue provides messages of high priority and is typically used for low latency messages. This queue can only be controlled by the owner of the subscriber.
#. **Subscriber’s control bus** : This bus allows other who have been given explicit write access by the owner of the subscriber to the bus to send control messages to the subscriber.
#. **Subscriber’s control queue** : This queue allows the subscriber to receive messages sent to the Subscriber’s control bus. This queue can only be controlled by the owner of the subscriber.

Each publisher after successful registration with CDX is provided with:

#. **Publisher’s public bus** : A bus where the publisher can send messages which any valid user can read.
#. **Publisher’s protected bus** : A bus where the publisher can send messages which can be read by a user to whom explicit permission has been given by the owner of the publisher.
#. **Publisher’s private bus** : A bus where the publisher can send messages which can only be read by the owner or the publisher itself.
#. **Publisher’s priority bus** : A bus where the publisher can send important messages, and can be read by an authorized user. This bus is used to publish low latency messages, and is typically subscribed using a priority queue of a subscriber.
#. **Publisher’s control bus** : A bus where any authorized user can send control messages for the publisher
#. **Publisher’s control queue** : A queue where control messages sent to the publisher can be read from.

