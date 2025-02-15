remove_definitions(-D__DEEPKS)
remove_definitions(-D__CUDA)
remove_definitions(-D__ROCM)
remove_definitions(-D__EXX)

install(DIRECTORY support DESTINATION ${CMAKE_CURRENT_BINARY_DIR})
install(FILES bcast_atom_pseudo_test.sh DESTINATION ${CMAKE_CURRENT_BINARY_DIR})
install(FILES bcast_atom_spec_test.sh DESTINATION ${CMAKE_CURRENT_BINARY_DIR})
install(FILES parallel_kpoints_test.sh DESTINATION ${CMAKE_CURRENT_BINARY_DIR})
install(FILES klist_test_para.sh DESTINATION ${CMAKE_CURRENT_BINARY_DIR})
install(FILES unitcell_test_parallel.sh DESTINATION ${CMAKE_CURRENT_BINARY_DIR})

AddTest(
  TARGET cell_read_pp
  LIBS ${math_libs} base device
  SOURCES read_pp_test.cpp ../read_pp.cpp ../read_pp_upf201.cpp ../read_pp_upf100.cpp ../read_pp_vwr.cpp ../read_pp_blps.cpp 
  ../../module_io/output.cpp
)

AddTest(
  TARGET cell_pseudo_nc
  LIBS ${math_libs} base device
  SOURCES pseudo_nc_test.cpp ../pseudo_nc.cpp ../read_pp.cpp ../read_pp_upf201.cpp ../read_pp_upf100.cpp ../read_pp_vwr.cpp 
  	../read_pp_blps.cpp ../../module_io/output.cpp
)

AddTest(
  TARGET cell_atom_pseudo
  LIBS ${math_libs} base device
  SOURCES atom_pseudo_test.cpp ../atom_pseudo.cpp ../pseudo_nc.cpp ../read_pp.cpp ../read_pp_upf201.cpp ../read_pp_upf100.cpp 
  	../read_pp_vwr.cpp ../read_pp_blps.cpp ../../module_io/output.cpp
)

AddTest(
  TARGET cell_atom_spec
  LIBS ${math_libs} base device
  SOURCES atom_spec_test.cpp ../atom_spec.cpp ../atom_pseudo.cpp ../pseudo_nc.cpp ../read_pp.cpp ../read_pp_upf201.cpp 
  	../read_pp_upf100.cpp ../read_pp_vwr.cpp ../read_pp_blps.cpp ../../module_io/output.cpp
)

AddTest(
  TARGET cell_klist_test
  LIBS ${math_libs} base device
  SOURCES klist_test.cpp ../klist.cpp ../parallel_kpoints.cpp ../../module_io/output.cpp ../module_symmetry/symm_other.cpp 
  	../module_symmetry/symmetry_basic.cpp ../module_symmetry/symmetry.cpp
)

AddTest(
  TARGET cell_klist_test_para1
  LIBS ${math_libs} base device
  SOURCES klist_test_para.cpp ../klist.cpp ../parallel_kpoints.cpp ../../module_io/output.cpp ../module_symmetry/symm_other.cpp 
  	../module_symmetry/symmetry_basic.cpp ../module_symmetry/symmetry.cpp
)

add_test(NAME cell_klist_test_para4
      COMMAND ${BASH} klist_test_para.sh
      WORKING_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}
)

AddTest(
  TARGET cell_ParaKpoints
  LIBS MPI::MPI_CXX
  SOURCES parallel_kpoints_test.cpp ../../module_base/global_variable.cpp ../../module_base/parallel_global.cpp 
  	../../module_base/parallel_common.cpp ../parallel_kpoints.cpp
)

find_program(BASH bash)

add_test(NAME cell_bcast_atom_pseudo_test
      COMMAND ${BASH} bcast_atom_pseudo_test.sh
      WORKING_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}
)

add_test(NAME cell_bcast_atom_spec_test
      COMMAND ${BASH} bcast_atom_spec_test.sh
      WORKING_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}
)

add_test(NAME cell_parallel_kpoints_test
      COMMAND ${BASH} parallel_kpoints_test.sh
      WORKING_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}
)

AddTest(
  TARGET cell_unitcell_test
  LIBS ${math_libs} base device
  SOURCES unitcell_test.cpp ../unitcell.cpp ../read_atoms.cpp ../read_cell_pseudopots.cpp ../atom_spec.cpp
	../atom_pseudo.cpp ../pseudo_nc.cpp ../read_pp.cpp ../read_pp_upf201.cpp ../read_pp_upf100.cpp
	../read_pp_vwr.cpp ../read_pp_blps.cpp ../../module_io/output.cpp
)

AddTest(
  TARGET cell_unitcell_test_readpp
  LIBS ${math_libs} base device
  SOURCES unitcell_test_readpp.cpp ../unitcell.cpp ../read_atoms.cpp ../read_cell_pseudopots.cpp ../atom_spec.cpp
	../atom_pseudo.cpp ../pseudo_nc.cpp ../read_pp.cpp ../read_pp_upf201.cpp ../read_pp_upf100.cpp
	../read_pp_vwr.cpp ../read_pp_blps.cpp ../../module_io/output.cpp
)

AddTest(
  TARGET cell_unitcell_test_para
  LIBS ${math_libs} base device
  SOURCES unitcell_test_para.cpp ../unitcell.cpp ../read_atoms.cpp ../read_cell_pseudopots.cpp ../atom_spec.cpp
	../atom_pseudo.cpp ../pseudo_nc.cpp ../read_pp.cpp ../read_pp_upf201.cpp ../read_pp_upf100.cpp
	../read_pp_vwr.cpp ../read_pp_blps.cpp ../../module_io/output.cpp
)

AddTest(
  TARGET cell_unitcell_test_setupcell
  LIBS ${math_libs} base device
  SOURCES unitcell_test_setupcell.cpp ../unitcell.cpp ../read_atoms.cpp ../read_cell_pseudopots.cpp ../atom_spec.cpp
	../atom_pseudo.cpp ../pseudo_nc.cpp ../read_pp.cpp ../read_pp_upf201.cpp ../read_pp_upf100.cpp
	../read_pp_vwr.cpp ../read_pp_blps.cpp ../../module_io/output.cpp
)

add_test(NAME cell_unitcell_test_parallel
      COMMAND ${BASH} unitcell_test_parallel.sh
      WORKING_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}
)
