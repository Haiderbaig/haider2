<?php
/*
  Template Name: Hotel Results
 */
?>
<?php get_header(); ?>
<?php if(isset($_POST["complaint_title"]) && isset($_POST["complaint_email"]) && isset($_POST["complaint_description"])): 
$post_id = submit_to_database($_POST["complaint_title"], $_POST["complaint_email"], $_POST["complaint_description"]);
// Mail user his complaint ID.
complaintNumberEmail($_POST["complaint_email"],$post_id);
?>
<div id="compMessage"><p class="compText">Your complaint Has been Registered Successfully, Please Check your email for complaint reference number.</p></div>
<?php endif; ?>
<div id="complaint_form">
<form id="compform" action="" method="POST">
    <div class="complaint_title">
        <label>Complaint Title:</label>
        <input id="thetitle" class="comp_title_inp" type="text" name="complaint_title" />
    </div>
    <div class="complaint_email">
        <label>Email:</label>
        <input class="comp_title_inp" type="text" name="complaint_email" />
    </div>
    <div class="complaint_description">
        <label>Complaint Description:</label>
        <textarea class="comp_title_inp comp_title_textarea" name="complaint_description"></textarea>
    </div>
    <div class="complaint_btn">
        <input id="submiter" type="submit" value="submit" />
    </div>
</form>
</div>
<!--<script type="text/javascript">
    jQuery(document).ready(function(){
    
    jQuery("#compform").submit(function(e){
       if(jQuery('input[name="complaint_title"]').val() == 0){
           alert("Complaint Title Cannont be Empty!");
       }else if(jQuery('input[name="complaint_email"]').val() == 0){
           alert("Complaint Email Cannont be Empty!");
       }
       e.preventDefault();
    });
        
    });
</script>-->

<?php get_footer(); ?>

