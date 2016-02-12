# StirFry-Staff
the custom staff archive page

<?php
 
/**
 * Template Name: Staff Archive
 * Description: Used as a page template to show page contents, followed by a loop through a CPT archive  
 */
 
remove_action ('genesis_loop', 'genesis_do_loop'); // Remove the standard loop
add_action( 'genesis_loop', 'custom_do_loop' ); // Add custom loop
 
function custom_do_loop() {
    	
	// Intro Text (from page content)
	echo '<div class="page hentry entry">';
        echo '<h1>StirFry Staff &amp; Facilitators</h1>' ;
	echo '<div class="entry-content">' . get_the_content() ;


	$args = array(
		'post_type' => 'staff', // enter your custom post type
                'staff-position' => 'facilitator' ,
		'orderby' => 'date',
		'order' => 'ASC',
		'posts_per_page'=> '45',  // overrides posts per page in theme settings
	);
	$loop = new WP_Query( $args );
	if( $loop->have_posts() ):
				
		while( $loop->have_posts() ): $loop->the_post(); global $post;
 
echo '<div class="allibox" >';
			echo '<div class="one-fourth first">';
			echo '<div class="staff-image"><a class="more-link" href="' . get_permalink() . '">'. get_the_post_thumbnail( $id, array(200,200) ).'</a></div>';
		
                     
			echo '</div>';	
			echo '<div class="three-fourths">';
			echo '<h3><a class="more-link" href="' . get_permalink() . '">' . get_the_title() . '</a></h3>';   
                        echo '<h5>' . genesis_get_custom_field( 'wpcf-title' ) . '</h5>'; //retrieve custom field   
                        echo '<h6>' . genesis_get_custom_field( 'wpcf-ethnicity' ) .'</h6>'; //retrieve custom field
			echo '<div class="bio_box">' . get_the_excerpt() . '</div>';

			echo '</div>'; 
echo '</div>';
		

		endwhile;
	
		
	endif;
	
	
	
	// Outro Text (hard coded)
	
	echo '</div><!-- end .entry-content -->';
	echo '</div><!-- end .page .hentry .entry -->';
}
	
/** Remove Post Info */
remove_action('genesis_before_post_content','genesis_post_info');
remove_action('genesis_after_post_content','genesis_post_meta');
 
genesis();
