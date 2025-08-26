set(Sources
		defs.cpp
		dist.cpp
		kmeans.cpp
		points_io.cpp
		metis_io.cpp
)

set (RoutingSources
		kmeans_tree_router.cpp
)

foreach(target IN LISTS TARGETS)
	target_sources(${target} PRIVATE ${Sources})
endforeach()

target_sources(Partition PRIVATE partitioning.cpp overlapping_partitioning.cpp kmeans_tree_router.cpp)

target_sources(QueryAttribution PRIVATE routes.cpp shard_searches.cpp route_search_combination.cpp kmeans_tree_router.cpp)

target_sources(SmallScaleQueries PRIVATE routes.cpp shard_searches.cpp route_search_combination.cpp kmeans_tree_router.cpp)

target_sources(Convert PRIVATE routes.cpp shard_searches.cpp route_search_combination.cpp kmeans_tree_router.cpp)

target_sources(GraphQualityBench PRIVATE partitioning.cpp)

target_sources(OracleRecall PRIVATE routes.cpp kmeans_tree_router.cpp)

target_sources(AnalyzeApproximationLosses PRIVATE routes.cpp kmeans_tree_router.cpp)

file(GLOB CPP_FILES "*.cpp")
add_library(partition_lib ${CPP_FILES})
target_include_directories(partition_lib PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})
target_link_libraries(partition_lib PUBLIC parlay kaminpar_shm)
