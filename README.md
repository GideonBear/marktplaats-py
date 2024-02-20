# marktplaats-py
A small Python package to request listings from marktplaats.nl. It supports python 3.7+.

## Installing
```shell
pip3 install marktplaats
```

## Example
This is an example on how to use the library:
```py
from marktplaats import SearchQuery, SortBy, SortOrder

search = SearchQuery("fiets", # Search query
                     zip_code="1016LV", # Zip code to base distance from
                     distance=100000, # Max distance from the zip code for listings
                     price_from=0, # Lowest price to search for
                     price_to=100, # Highest price to search for
                     limit=5, # Max listings (page size, max 25)
                     offset=0, # Offset for listings (page * limit)
                     sort_by=SortBy.OPTIMIZED, # DATE, PRICE, LOCATATION, OPTIMIZED
                     sort_order=SortOrder.ASC) # ASCending or DESCending

listings = search.get_listings()

for listing in listings:
    print(listing.title)
    print(listing.description)
    print(listing.price)
    print(listing.link)
    
    # the location object
    print(listing.location)
    
    # the seller object
    print(listing.seller)
    
    # the datetime object
    print(listing.date)
    
    # the full seller object (another request)
    print(listing.seller.get_seller())
    
    for image in listing.images:
        print(image.medium)
    
    
    print("-----------------------------")
```