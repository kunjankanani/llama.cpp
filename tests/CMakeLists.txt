function(llama_add_test source)
    get_filename_component(TEST_TARGET ${source} NAME_WE)
    add_executable(${TEST_TARGET} ${source})
    install(TARGETS ${TEST_TARGET} RUNTIME)
    target_link_libraries(${TEST_TARGET} PRIVATE llama)
    add_test(NAME ${TEST_TARGET} COMMAND $<TARGET_FILE:${TEST_TARGET}> ${ARGN})
endfunction()

# llama_add_test(test-double-float.c) # SLOW
llama_add_test(test-quantize-fns.cpp)
llama_add_test(test-quantize-perf.cpp)
llama_add_test(test-sampling.cpp)
llama_add_test(test-tokenizer-0.cpp ${CMAKE_CURRENT_SOURCE_DIR}/../models/ggml-vocab.bin)
llama_add_test(test-grad0.c) # SLOW
# llama_add_test(test-opt.c) # SLOW
