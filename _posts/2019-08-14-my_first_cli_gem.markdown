---
layout: post
title:      "My First CLI Gem"
date:       2019-08-14 21:37:41 +0000
permalink:  my_first_cli_gem
---


Welcome to my first project. It was such a a journey. For this project I am scraping the https://www.fonehouse.co.uk for the best offer on an iPhone and prompting the user to choose from a list of 11 phones(currently) to see more details on. I have watched a lot of tutorials on learn videos on the CLI section which I found very useful. If you just about to start working on the project, I know it can feel overwhelming at times and I also know that what I am about to say sounds like a cliché but keep going little by little and you will get there. I choose to do mine in the IDE Sandbox(which you will find in a lot of places, I always opened mine from the Welcome section in the curriculum).

In the terminal type bundle gem and the name of your project(snake case). For example for my project I would type **bundle gem best_iphone_offers**. You will be prompted with three questions: 
1. Do you want to generate test files? On this occassion, choose 'no',  generally you would write tests as well but we are not there yet. If you are also writing tests, you are a rockstar!
2. Do you want to licence your code? 'yes'
3. Do you want to include code on conduct? 'yes'

Before starting the project, you should be familar with the structure of a [CLI](https://learn.co/tracks/full-stack-web-development-v5/intro-to-ruby-development/command-line-applications/cli-applications-in-ruby). The next step for me was to think about how many classes I would need to start my project, I though I should definitely have a scraper class, a cli and an offer. Three was all I needed for my project. I followed Beth's instructions on the Eden project tutorial to set everything up https://instruction.learn.co/student/video_lectures#/472. I learned that the scraper.rb class should only be responsible for scraping. Mine looks like this:

> class BestIphoneOffer::Scraper 
>   
>   def self.get_page
>     Nokogiri::HTML(open("https://www.fonehouse.co.uk/brand/apple-mobile-phone-deals"))
>   end
>   
>   def self.scrape_offers
>     handset = get_page.css('div#filterResults div.deal-box')
>     
>     handset.each do |handset|
>       name = handset.css('span.handset').text.gsub("Apple","").strip
>       upfront_cost = handset.css('span.normal').text.downcase.gsub("from", "contract")
>       price = handset.css('div.contract.cost.mx-auto.mx-sm-0').text
>       contract_length = handset.css('div.length').text
>       BestIphoneOffer::Offer.new(name, upfront_cost, price, contract_length)
>     end
>     
>   end
> 

The offer.rb class should have as attr_accesor what I am interested to scrape from the webpage - name of the phone, upfront cost, price and the contract lenght which should also be initialized. Also I should also have a @@all where I push all the offers. The find method will be also called in my CLI to help me get the offer that the user wants to see. 

> class BestIphoneOffer::Offer 
>   attr_accessor :name, :upfront_cost, :price, :contract_length
>   
>   @@all = []
>   
>   def initialize(name, upfront_cost, price, contract_length)
>     @name = name
>     @upfront_cost = upfront_cost
>     @price = price
>     @contract_length = contract_length
>     save
>   end
>   
>   def self.all
>     @@all
>   end
>   
>   def self.find(input)
>     self.all[input.to_i - 1]
>   end
>   
>   def save
>     @@all << self
>   end
>   
> end

 
Finally my cli.rb class. I started my gem with the scraper class. For me that was one of the most complicated parts of the project. I had to make sure this 'works' first. Next 

> def call
> 	    puts "\nWelcome! Here are the best iPhone offers at the moment:\n"
> 	    BestIphoneOffer::Scraper.scrape_offers
>       list_offer
>       menu
> 	  end 
> 
>     def list_offer
> 	     BestIphoneOffer::Offer.all.each.with_index(1) do |handset, idx|
> 	       puts "#{idx} #{handset.name}"
> 	     end
> 	  end
> 	 
> 	  def menu
> 	   puts "\nPlease choose an offer from the list to see the details.\n"
> 	   puts "Type 'list' to see the offers again or 'exit' to exit."
> 	   puts ""
> 	   input = gets.strip.downcase
> 	   puts ""
> 	     if input != "exit" && (input.to_i-1).between?(0, BestIphoneOffer::Offer.all.size - 1)
> > 	      offer = BestIphoneOffer::Offer.find(input)
> 	      puts "For the #{offer.name} you will have a #{offer.upfront_cost} at #{offer.price} #{offer.contract_length}." 
> 	       menu
> 	     elsif input == "exit"
> 	       goodbye
> 	     elsif input == "list"
> 	       list_offer
> 	       menu
> 	     else
> 	        puts "\nPlease enter a number between 1 and #{BestIphoneOffer::Offer.all.size} \n"
> 	       menu
> 	     end
> 	   end 
> 	  
> 	 def goodbye
> 	  puts "\nThank you for checking Best iPhone Offers!\n"
> 	  puts "
>              .:'
>       __ :'__
>    .'`__`-'__``.
>   :__________.-'
>   :_________:
>    :_________`-;
>     `.__.-.__.'
>     "
> 	 end
> 	end 

I started my gem with the scraper class. For me that was one of the most complicated parts of the project. I had to make sure this 'works' first. I continued with the offer.rb class. The last one was the cli.rb and I know its a bit backwards but that was my way of approaching it. 

It was such a challenge and I would lie to say that I was positive and full of pasion throughout. There were a few very frustrating moments. I think that is the most difficult part about learning how to code, at least for me, it that is all very up and down and although I was aware of that when I started the course, it is very easy to forget when you are working on your very first project and things dont go as planned. On a happier note, working on my first gem helped me to better understand key concepts in OO ruby and ruby in general. And now the most exciting part, now that I am about to submit my project, I want to work on another gem, this time enthusiastically :-) so I guess I found the passion.

