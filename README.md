# nosql-challenge

###### CODE GIVEN IN MODULE LESSONS

# Write an aggregation query that counts the number of documents, grouped by "country"
query = [{'$group': {'_id': "$country", 'count': { '$sum': 1 }}}]

# Run the query with the aggregate method and save the results to a variable
results = list(artifacts.aggregate(query))

# Print the number of countries in the result
print("Number of countries in result: ", len(results))

# Build the aggregation pipeline
# Write a match query to find only the documents about artifacts that have a width greater than or equal to 40cm.
match_query = {'$match': {'measurements.elementMeasurements.Width': {'$gte': 40}}}

# Write an aggregation query that counts the number of documents, grouped by "country"
group_query = {'$group': {'_id': "$country", 'count': { '$sum': 1 }}}

# Create a dictionary that will allow the pipeline to sort by count in descending order
sort_values = {'$sort': { 'count': -1 }}

# Put the pipeline together
pipeline = [match_query, group_query, sort_values]

# Build the aggregation pipeline
# Write a match query to find only the documents about artifacts that
# have a classification where "Wood" is the value.
match_query = {'$match': {'classification': {'$regex': "Wood"}}}

# Write an aggregation query that counts the number of documents and finds the maximum height,
# grouped by "classification"
group_query = {'$group': {'_id': "$classification", 
                          'count': { '$sum': 1 },
                          'max_height': { '$max': '$measurements.elementMeasurements.Height' }}}

# Create a dictionary that will allow the pipeline to sort by count in descending order, 
# then sort by classification in alphabetical order
sort_values = {'$sort': { 'count': -1, '_id': 1 }}

# Put the pipeline together
pipeline = [match_query, group_query, sort_values]
# Select only the mechanic_name and wages.hourly_rate fields from the mechanics collection
query = {}
fields = {'mechanic_name': 1, 'wages.hourly_rate': 1}

# Capture the results to a variable
results = mechanics.find(query, fields)

# Pretty print the results
for result in results:
    pprint(result)

