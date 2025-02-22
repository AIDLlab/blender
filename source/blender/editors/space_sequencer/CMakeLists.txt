# SPDX-FileCopyrightText: 2023 Blender Authors
#
# SPDX-License-Identifier: GPL-2.0-or-later

set(INC
  ../include
  ../../blenkernel
  ../../blenloader
  ../../blentranslation
  ../../draw
  ../../gpu
  ../../makesrna
  ../../sequencer
  ../../windowmanager

  # RNA_prototypes.h
  ${CMAKE_BINARY_DIR}/source/blender/makesrna
)

set(INC_SYS
)

set(SRC
  sequencer_add.cc
  sequencer_buttons.cc
  sequencer_channels_draw.cc
  sequencer_channels_edit.cc
  sequencer_drag_drop.cc
  sequencer_edit.cc
  sequencer_modifier.cc
  sequencer_ops.cc
  sequencer_preview.cc
  sequencer_preview_draw.cc
  sequencer_proxy.cc
  sequencer_retiming.cc
  sequencer_retiming_draw.cc
  sequencer_scopes.cc
  sequencer_select.cc
  sequencer_thumbnails.cc
  sequencer_timeline_draw.cc
  sequencer_view.cc
  space_sequencer.cc

  sequencer_intern.hh
)

set(LIB
  PRIVATE bf::blenfont
  PRIVATE bf::blenlib
  PRIVATE bf::depsgraph
  PRIVATE bf::dna
  bf_editor_interface
  bf_editor_util
  PRIVATE bf::imbuf
  PRIVATE bf::intern::atomic
  PRIVATE bf::intern::guardedalloc
)

if(WITH_AUDASPACE)
  list(APPEND INC_SYS
    ${AUDASPACE_C_INCLUDE_DIRS}
  )
  if(WITH_SYSTEM_AUDASPACE)
    list(APPEND LIB
      ${AUDASPACE_C_LIBRARIES}
      ${AUDASPACE_PY_LIBRARIES}
    )
  endif()
  add_definitions(-DWITH_AUDASPACE)
endif()


blender_add_lib(bf_editor_space_sequencer "${SRC}" "${INC}" "${INC_SYS}" "${LIB}")

# RNA_prototypes.h dna_type_offsets.h
add_dependencies(bf_editor_space_sequencer bf_rna)
