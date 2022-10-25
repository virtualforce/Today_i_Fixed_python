# Problem
In order to manage and view data for tables properly, we need to add pagination to structures so that data can be viewed in a proper manner.
How to add pagination in bootstrap tables?


# Environment
HTML,CSS,Javascript, Bootstrap


# How you fix it
By including components in CSS and javascript to properly manage the data and show them to end user in the form of pages. The basic structure of bootstrap tables does not allow us to show the data in paginated form we need to include extra css and javascript modules to make the job easier.
The code snippet for performing this function is attached below


# Solution
The html snippet for paginated table is as shown below:

```<div class="card-header">
          <h5>Details of Document Scan</h5>

              <div class="num_rows">

                      <div class="form-group"> 	<!--		Show Numbers Of Rows 		-->
                           <select class  ="form-control" name="state" id="maxRows">
                               <option value="10">10</option>
                               <option value="15">15</option>
                               <option value="20">20</option>
                               <option value="50">50</option>
                               <option value="70">70</option>
                               <option value="100">100</option>
                              <option value="5000">Show ALL Rows</option>
                              </select>

                        </div>
              </div
        </div>
      <table class="table table-hover" id= "table-id" style="transform: translateX(-20px);">
          <thead>
          <tr> 
            <!-- The remaining code for table -->
            </tr>
        </thead>
       </table>
        <div class='pagination-container'>
              <nav>
                <ul class="pagination">
                 <!--	Here the JS Function Will Add the Rows -->
                </ul>
              </nav>
          </div>
      <div class="rows_count">Showing 11 to 20 of 91 entries</div>        
  </div>

  
  The javascript snippet of code is attached below:
	

<div class="card-header">
  <script>
    getPagination('#table-id');
	$('#maxRows').trigger('change');
	function getPagination (table){

		  $('#maxRows').on('change',function(){
		  	$('.pagination').html('');				// reset pagination div
		  	var trnum = 0 ;						// reset tr counter 
		  	var maxRows = parseInt($(this).val());			// get Max Rows from select option
        
		  	var totalRows = $(table+' tbody tr').length;		// numbers of rows 
			 $(table+' tr:gt(0)').each(function(){			// each TR in  table and not the header
			 	trnum++;					// Start Counter 
			 	if (trnum > maxRows ){				// if tr number gt maxRows
			 		
			 		$(this).hide();				// fade it out 
			 	}if (trnum <= maxRows ){$(this).show();}        // else fade in
			 });
											
			 if (totalRows > maxRows){				// if tr total rows gt max rows option
			 	var pagenum = Math.ceil(totalRows/maxRows);	// ceil total(rows/maxrows) to get ..  
			 							// numbers of pages 
			 	for (var i = 1; i <= pagenum ;){		// for each page append pagination li 
			 	
				$('.pagination').append('<li data-page="'+i+'">\
				<span>'+ i++ +'<span class="sr-only">(current)</span></span>\
				</li>').show();
			 	}						// end for i 
			} 							// end if row count > max rows

			$('.pagination li:first-child').addClass('active'); // add active class to the first li 

        //SHOWING ROWS NUMBER OUT OF TOTAL DEFAULT
       showig_rows_count(maxRows, 1, totalRows);
        $('.pagination li').on('click',function(e){		                // on click each page
        e.preventDefault();
				var pageNum = $(this).attr('data-page');	// get it's number
				var trIndex = 0 ;				// reset tr counter
				$('.pagination li').removeClass('active');	// remove active class from all li 
				$(this).addClass('active');			// add active class to the clicked 
         showig_rows_count(maxRows, pageNum, totalRows);
				 $(table+' tr:gt(0)').each(function(){		// each tr in table not the header
				 	trIndex++;				// tr index counter 

				 	// if tr index gt maxRows*pageNum or lt maxRows*pageNum-maxRows fade if out
				 	if (trIndex > (maxRows*pageNum) || trIndex <= ((maxRows*pageNum)-maxRows)){
				 		$(this).hide();		
				 	}else {$(this).show();} 		//else fade in 
				 }); 						// end of for each tr in table
			});							// end of on click pagination list
		});
	}		

</script>
</div>          
```
