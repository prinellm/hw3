/*
 * mm_alloc.c
 *
 * mm_free: takes in a ptr and allocates the (ptr-block size) as the new address for the ptr. Makes the block equal to the new address( i.e the ptr) and frees the block. If the block is at the end of the heap then the brk is moved to the previous block.

 */

#include "mm_alloc.h"

#include <stdlib.h>

/* Your final implementation should comment out this macro. */
#define MM_USE_STUBS
s_block_ptr findFirst(s_block_ptr * lastBlock, size_t size);
//struct rlimit limit;
void *first = NULL;


void* mm_malloc(size_t size)
{
#ifdef MM_USE_STUBS
    return calloc(1, size);
#else
#error Not implemented.
#endif

    s_block_ptr block, last;



	if (first==NULL) {

	  last = first;

	s_block_ptr block = first;

	while(block && !(block->free && block->size >= size))
	{
		last = block;
		block = block->next;
	}
	 

	  if (block) {

	    if ((block->size - size) >= ( BLOCK_SIZE + 4))
{
	s_block_ptr newBlock;

	newBlock = (s_block_ptr) block->data + size;
	newBlock->size = block->size -size -BLOCK_SIZE;
	newBlock->next = block->next;
	newBlock->prev = block;
	newBlock->free = 1;
	newBlock->ptr = newBlock->data;

	block->size = size;
	block->next = newBlock;

	if(newBlock->next)
	{
		newBlock->next->prev = newBlock;
	}
}	    


	  block->free =0;
	} 

	else {

	  block = extend_heap (last ,size);

	  if (!block)
	    return (NULL );
	  }

	} 

	else {

	  block = extend_heap (NULL ,size);
	
	  if (!block)
	    return (NULL );

	 first = block;
	}

	return (block->data );




}

void* mm_realloc(void* ptr, size_t size)
{
/*#ifdef MM_USE_STUBS
    return realloc(ptr, size);
#else
#error Not implemented.
#endif*/

    void * reallocate;
    reallocate = mm_malloc(size);
    memcpy(reallocate, ptr, size);

    return reallocate;
}

void mm_free(void* ptr)
{
/*#ifdef MM_USE_STUBS
    free(ptr);
#else
#error Not implemented.
#endif*/

s_block_ptr block;
char *newAddress;
	newAddress = ptr;

	newAddress = newAddress - BLOCK_SIZE;

	ptr = newAddress;


    block = ptr;
    block->free = 1;

    if( (block ->prev) && (block->prev->free=1) )
    {
s_block_ptr prevBlock;
 if( (prevBlock->next) && (prevBlock->next->free=1) )
  {
  	prevBlock->size = prevBlock->size + BLOCK_SIZE + prevBlock->next->size;
  	prevBlock->next = prevBlock->next->next;

  	if(prevBlock->next)
  		prevBlock->next->prev = prevBlock;
  

    	block = prevBlock;
    }
}
    if(block -> next)
    {
 if( (block->next) && (block->next->free=1) )
  {
  	block->size = block->size + BLOCK_SIZE + block->next->size;
  	block->next = block->next->next;

  	if(block->next)
  		block->next->prev = block;
  
    	
    }
}
    else{
    	if(block ->prev)
    		block->prev->next = NULL;
    	else
    		first = NULL;

    	brk(block);
    }
}

s_block_ptr extend_heap (s_block_ptr last , size_t s)
{
	int status;
	s_block_ptr block;

	block = sbrk(0);

	status = (long)sbrk(BLOCK_SIZE + s);

	if(status < 0)
	{
		return NULL;
	}

	block->size = s;
	block->prev = last;
	block->next = NULL;
	block->ptr = block->data;

	if(last)
	{
		last->next = block;
	}
	block->free = 0;

	return block;

}

