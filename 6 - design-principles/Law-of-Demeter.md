# Least Knowledge (Law of Demeter)
Talk only to your immediate friends.

Only invoke methods that belongs to:

- The object itself
- Objects passed in as a parameter to the method
- Any object the method creates or instantiates
- Any components of the object
