# logstash-mongo-elastic

## Download Logstash for MAC

    [https://www.elastic.co/downloads/logstash](https://www.elastic.co/downloads/logstash)
    
    
Install Mongo-Input Plugin:

    bin/logstash-plugin install logstash-input-mongodb
    

Create Config File: config/logstash-mongo.conf


          input {
              mongodb{
            uri => 'mongodb://localhost:27017/eshop?directConnection=true'
            placeholder_db_dir => '/opt/logstash3-mongodb/'
            placeholder_db_name => 'logstash3_sqlite.db'
            collection => 'products'
            batch_size => 5000
                }
            }
          filter {
            mutate {
            copy => { "_id" => "[@metadata][_id]"}
            remove_field => ["_id"]
                    }
           }
           output {
                    stdout {
                            codec => rubydebug
                    }
                    elasticsearch {
                            action => "index"
                            index => "products"
                            hosts => ["localhost:9200"]
                            user => "elastic"
                            password => "bVyKWe018bw5fLh5wiH8"
                    }
            }




Run Below Command from Logstash Home Folder:

            bin/logstash -f config/logstash-mongo.conf
            
            
Install ElasticVue from chrome Extension:



                Check the Indices for Products
                
                <img width="1718" alt="image" src="https://user-images.githubusercontent.com/109475849/205901850-458d19bf-4159-47a5-8c40-529b98bc309f.png">

