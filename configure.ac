AC_INIT(
    [arc-theme-tomorrow],
    [20210204],
    [https://github.com/janebuoy/arc-theme-tomorrow/issues],
    [arc-theme-tomorrow],
    [https://github.com/janebuoy/arc-theme-tomorrow]
)

AC_CONFIG_AUX_DIR([build-aux])
AC_CONFIG_MACRO_DIR([m4])
AM_INIT_AUTOMAKE([no-dist-gzip dist-xz foreign])
AC_PROG_LN_S
AC_PROG_MKDIR_P

ARC_ENABLE([LIGHT],         [light],         [Arc Tomorrow Light],     	[disable])
ARC_ENABLE([DARKER],        [darker],        [Arc Tomorrow Darker],    	[disable])
ARC_ENABLE([DARK],          [dark],          [Arc Tomorrow Dark],      	[disable])
ARC_ENABLE([LIGHTER],       [lighter],       [Arc Tomorrow Lighter],   	[disable])
ARC_ENABLE([CINNAMON],      [cinnamon],      [Cinnamon],      		[disable])
ARC_ENABLE([GNOME_SHELL],   [gnome-shell],   [GNOME Shell],   		[disable])
ARC_ENABLE([GTK2],          [gtk2],          [GTK2],          		[disable])
ARC_ENABLE([GTK3],          [gtk3],          [GTK3],          		[disable])
ARC_ENABLE([METACITY],      [metacity],      [Metacity],      		[disable])
ARC_ENABLE([UNITY],         [unity],         [Unity],         		[disable])
ARC_ENABLE([XFWM],          [xfwm],          [XFWM],          		[disable])
ARC_ENABLE([TRANSPARENCY],  [transparency],  [transparency],  		[disable])
ARC_ENABLE([PLANK],         [plank],         [Plank theme],   		[disable])

AS_IF([test "x$ENABLE_TRANSPARENCY" != xno], [
    AC_SUBST([themedir], [${datadir}/themes/Arc-Tomorrow])
    AC_SUBST([themedarkerdir], [${datadir}/themes/Arc-Tomorrow-Darker])
    AC_SUBST([themedarkdir], [${datadir}/themes/Arc-Tomorrow-Dark])
    AC_SUBST([themelighterdir], [${datadir}/themes/Arc-Tomorrow-Lighter])
], [
    AC_SUBST([themedir], [${datadir}/themes/Arc-Tomorrow-solid])
    AC_SUBST([themedarkerdir], [${datadir}/themes/Arc-Tomorrow-Darker-solid])
    AC_SUBST([themedarkdir], [${datadir}/themes/Arc-Tomorrow-Dark-solid])
    AC_SUBST([themelighterdir], [${datadir}/themes/Arc-Tomorrow-Lighter-solid])
])

AS_IF([test "x$ENABLE_GTK3" != xno], [ARC_GTK3])
AS_IF([test "x$ENABLE_GNOME_SHELL" != xno],
    [ARC_GNOME_SHELL]
    [GNOME_SHELL_VERSMNR=`echo $GNOME_SHELL_VERSION | cut -d. -f2`])
AM_CONDITIONAL([GNOME_SHELL_3_32_OR_NEWER], [test "0$GNOME_SHELL_VERSMNR" -ge 31])
AS_IF([test "x$ENABLE_CINNAMON" != xno], [ARC_CINNAMON])

AS_IF([test "x$ENABLE_GTK2" != xno -o "x$ENABLE_GTK3" != xno -o "x$ENABLE_XFWM" != xno], [
    AC_PATH_PROG([INKSCAPE], [inkscape])
    AS_IF([test "x$ac_cv_path_INKSCAPE" = x], [AC_MSG_ERROR([inkscape not found])])
    AS_IF([test "x$ac_cv_path_INKSCAPE" != x],
        [INKSCAPE_VERSMJR=`inkscape --version 2> /dev/null | cut -d' ' -f2 | cut -d'.' -f1`]
    )
    AC_PATH_PROG([OPTIPNG], [optipng])
    AS_IF([test "x$ac_cv_path_OPTIPNG" = x], [AC_MSG_WARN([optipng not found, PNG assets won't be optimized])])
])
AM_CONDITIONAL([INKSCAPE_1_0_OR_NEWER], [test "x$INKSCAPE_VERSMJR" = x1])
AM_CONDITIONAL([OPTIPNG], [test ! "x$ac_cv_path_OPTIPNG" = x])

AS_IF([test "x$ENABLE_GTK3" != xno -o "x$ENABLE_CINNAMON" != xno -o "x$ENABLE_GNOME_SHELL" != xno], [
    AC_PATH_PROG([SASSC], [sassc])
    AS_IF([test "x$ac_cv_path_SASSC" = x], [AC_MSG_ERROR([sassc not found])])
])

AC_CONFIG_FILES([
    common/gtk-2.0/Makefile
    common/gtk-3.0/Makefile
    common/gtk-3.0/3.18/Makefile
    common/gtk-3.0/3.20/Makefile
    common/gtk-3.0/3.22/Makefile
    common/gtk-3.0/3.24/Makefile
    common/xfwm4/Makefile
    common/Makefile
    Makefile
])

AC_OUTPUT
