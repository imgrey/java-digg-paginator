java-digg-paginator
===================

Provides digg-style pagination functionality

See pagination.png

Usage example:

	Integer itemsCount = dotaItemCatalogDAO.getItemsCount();
	Integer itemsPerPage = 10;

	PagingSpecification pagingSpec = new PagingSpecification(itemsCount, itemsPerPage, itemsPerPage/5);
	PageSpecification pageSpec;

	try{
		pageSpec = pagingSpec.getPageSpecification(pageNumber);
	} catch (IllegalArgumentException e){
		if(logger.isDebugEnabled()){
			...
		}
		throw new ResourceNotFoundException();
	}

	Integer offset = pageSpec.getOffset();
	Integer limit = pageSpec.getLimit();

	Iterator<ItemObject> iter = dotaItemCatalogDAO.getItems(offset, limit).iterator();

	List<ItemObject> objectList = new ArrayList<ItemObject>();
	while(iter.hasNext()){
		ItemObject obj = iter.next();
			
		objectList.add(obj);
	}
	pagingSpec.setObjectList(objectList);


See https://github.com/imgrey/java-digg-style-paginator-example for working example.
