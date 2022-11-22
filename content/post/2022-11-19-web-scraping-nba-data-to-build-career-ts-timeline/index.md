---
title: "Web Scraping NBA Data from Basketball Reference"
author: "Zachary Shelly"
date: "2022-11-19"
slug: "web-scraping-nba-data-from-basketball-reference"
categories: []
tags: []
---

This is the webscraping process.

``` r
url <- paste0("https://www.basketball-reference.com/leagues/NBA_2023_standings.html")
webpage <- read_html(curl(url, handle = curl::new_handle("useragent" = "just.a.little.project")))

#creating the Eastern Conference Standings table
col_names <- webpage %>%
  html_nodes(paste("#confs_standings_E .poptip")) %>% #I got this by using  the selector gadget plugin
  html_attr("data-stat")


data <- webpage %>%
  html_nodes(paste("#confs_standings_E .full_table .right , #confs_standings_E .full_table .left")) %>% #I got this by using  the selector gadget plugin
  html_text()

data <- data %>% matrix(ncol = length(col_names), byrow = TRUE)
eastern_conf_standings <- as.data.frame(data)
names(eastern_conf_standings) <- col_names

#creating the Western Conference Standings table
col_names <- webpage %>%
  html_nodes(paste("#confs_standings_W .poptip")) %>% #I got this by using  the selector gadget plugin
  html_attr("data-stat")


data <- webpage %>%
  html_nodes(paste("#confs_standings_W .full_table .right , #confs_standings_W .full_table .left")) %>% #I got this by using  the selector gadget plugin
  html_text()

data <- data %>% matrix(ncol = length(col_names), byrow = TRUE)
western_conf_standings <- as.data.frame(data)
names(western_conf_standings) <- col_names
```

This is me trying out the gtExtras package for the first time.

``` r
western_conf_standings %>% gt() %>% gt_theme_nytimes() %>% tab_header(title = "Western Conference")
```

<div id="qpfyrmfciw" style="padding-left:0px;padding-right:0px;padding-top:10px;padding-bottom:10px;overflow-x:auto;overflow-y:auto;width:auto;height:auto;">
<style>@import url("https://fonts.googleapis.com/css2?family=Source+Sans+Pro:ital,wght@0,100;0,200;0,300;0,400;0,500;0,600;0,700;0,800;0,900;1,100;1,200;1,300;1,400;1,500;1,600;1,700;1,800;1,900&display=swap");
@import url("https://fonts.googleapis.com/css2?family=Libre+Franklin:ital,wght@0,100;0,200;0,300;0,400;0,500;0,600;0,700;0,800;0,900;1,100;1,200;1,300;1,400;1,500;1,600;1,700;1,800;1,900&display=swap");
@import url("https://fonts.googleapis.com/css2?family=Source+Sans+Pro:ital,wght@0,100;0,200;0,300;0,400;0,500;0,600;0,700;0,800;0,900;1,100;1,200;1,300;1,400;1,500;1,600;1,700;1,800;1,900&display=swap");
html {
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Helvetica Neue', 'Fira Sans', 'Droid Sans', Arial, sans-serif;
}

#qpfyrmfciw .gt_table {
  display: table;
  border-collapse: collapse;
  margin-left: auto;
  margin-right: auto;
  color: #333333;
  font-size: 16px;
  font-weight: normal;
  font-style: normal;
  background-color: #FFFFFF;
  width: auto;
  border-top-style: none;
  border-top-width: 2px;
  border-top-color: #A8A8A8;
  border-right-style: none;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #A8A8A8;
  border-left-style: none;
  border-left-width: 2px;
  border-left-color: #D3D3D3;
}

#qpfyrmfciw .gt_heading {
  background-color: #FFFFFF;
  text-align: left;
  border-bottom-color: #FFFFFF;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
}

#qpfyrmfciw .gt_caption {
  padding-top: 4px;
  padding-bottom: 4px;
}

#qpfyrmfciw .gt_title {
  color: #333333;
  font-size: 125%;
  font-weight: initial;
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 5px;
  padding-right: 5px;
  border-bottom-color: #FFFFFF;
  border-bottom-width: 0;
}

#qpfyrmfciw .gt_subtitle {
  color: #333333;
  font-size: 85%;
  font-weight: initial;
  padding-top: 0;
  padding-bottom: 6px;
  padding-left: 5px;
  padding-right: 5px;
  border-top-color: #FFFFFF;
  border-top-width: 0;
}

#qpfyrmfciw .gt_bottom_border {
  border-bottom-style: none;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
}

#qpfyrmfciw .gt_col_headings {
  border-top-style: none;
  border-top-width: 2px;
  border-top-color: #D3D3D3;
  border-bottom-style: none;
  border-bottom-width: 1px;
  border-bottom-color: #334422;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
}

#qpfyrmfciw .gt_col_heading {
  color: #333333;
  background-color: #FFFFFF;
  font-size: 12px;
  font-weight: normal;
  text-transform: inherit;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
  vertical-align: bottom;
  padding-top: 5px;
  padding-bottom: 6px;
  padding-left: 5px;
  padding-right: 5px;
  overflow-x: hidden;
}

#qpfyrmfciw .gt_column_spanner_outer {
  color: #333333;
  background-color: #FFFFFF;
  font-size: 12px;
  font-weight: normal;
  text-transform: inherit;
  padding-top: 0;
  padding-bottom: 0;
  padding-left: 4px;
  padding-right: 4px;
}

#qpfyrmfciw .gt_column_spanner_outer:first-child {
  padding-left: 0;
}

#qpfyrmfciw .gt_column_spanner_outer:last-child {
  padding-right: 0;
}

#qpfyrmfciw .gt_column_spanner {
  border-bottom-style: none;
  border-bottom-width: 1px;
  border-bottom-color: #334422;
  vertical-align: bottom;
  padding-top: 5px;
  padding-bottom: 5px;
  overflow-x: hidden;
  display: inline-block;
  width: 100%;
}

#qpfyrmfciw .gt_group_heading {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: initial;
  text-transform: inherit;
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
  vertical-align: middle;
  text-align: left;
}

#qpfyrmfciw .gt_empty_group_heading {
  padding: 0.5px;
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: initial;
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  vertical-align: middle;
}

#qpfyrmfciw .gt_from_md > :first-child {
  margin-top: 0;
}

#qpfyrmfciw .gt_from_md > :last-child {
  margin-bottom: 0;
}

#qpfyrmfciw .gt_row {
  padding-top: 7px;
  padding-bottom: 7px;
  padding-left: 5px;
  padding-right: 5px;
  margin: 10px;
  border-top-style: solid;
  border-top-width: 1px;
  border-top-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
  vertical-align: middle;
  overflow-x: hidden;
}

#qpfyrmfciw .gt_stub {
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: initial;
  text-transform: inherit;
  border-right-style: solid;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
  padding-left: 5px;
  padding-right: 5px;
}

#qpfyrmfciw .gt_stub_row_group {
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: initial;
  text-transform: inherit;
  border-right-style: solid;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
  padding-left: 5px;
  padding-right: 5px;
  vertical-align: top;
}

#qpfyrmfciw .gt_row_group_first td {
  border-top-width: 2px;
}

#qpfyrmfciw .gt_summary_row {
  color: #333333;
  background-color: #FFFFFF;
  text-transform: inherit;
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
}

#qpfyrmfciw .gt_first_summary_row {
  border-top-style: solid;
  border-top-color: #D3D3D3;
}

#qpfyrmfciw .gt_first_summary_row.thick {
  border-top-width: 2px;
}

#qpfyrmfciw .gt_last_summary_row {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
}

#qpfyrmfciw .gt_grand_summary_row {
  color: #333333;
  background-color: #FFFFFF;
  text-transform: inherit;
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
}

#qpfyrmfciw .gt_first_grand_summary_row {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  border-top-style: double;
  border-top-width: 6px;
  border-top-color: #D3D3D3;
}

#qpfyrmfciw .gt_striped {
  background-color: rgba(128, 128, 128, 0.05);
}

#qpfyrmfciw .gt_table_body {
  border-top-style: none;
  border-top-width: 2px;
  border-top-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #FFFFFF;
}

#qpfyrmfciw .gt_footnotes {
  color: #333333;
  background-color: #FFFFFF;
  border-bottom-style: none;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 2px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
}

#qpfyrmfciw .gt_footnote {
  margin: 0px;
  font-size: 90%;
  padding-left: 4px;
  padding-right: 4px;
  padding-left: 5px;
  padding-right: 5px;
}

#qpfyrmfciw .gt_sourcenotes {
  color: #333333;
  background-color: #FFFFFF;
  border-bottom-style: none;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 2px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
}

#qpfyrmfciw .gt_sourcenote {
  font-size: 90%;
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 5px;
  padding-right: 5px;
}

#qpfyrmfciw .gt_left {
  text-align: left;
}

#qpfyrmfciw .gt_center {
  text-align: center;
}

#qpfyrmfciw .gt_right {
  text-align: right;
  font-variant-numeric: tabular-nums;
}

#qpfyrmfciw .gt_font_normal {
  font-weight: normal;
}

#qpfyrmfciw .gt_font_bold {
  font-weight: bold;
}

#qpfyrmfciw .gt_font_italic {
  font-style: italic;
}

#qpfyrmfciw .gt_super {
  font-size: 65%;
}

#qpfyrmfciw .gt_footnote_marks {
  font-style: italic;
  font-weight: normal;
  font-size: 75%;
  vertical-align: 0.4em;
}

#qpfyrmfciw .gt_asterisk {
  font-size: 100%;
  vertical-align: 0;
}

#qpfyrmfciw .gt_indent_1 {
  text-indent: 5px;
}

#qpfyrmfciw .gt_indent_2 {
  text-indent: 10px;
}

#qpfyrmfciw .gt_indent_3 {
  text-indent: 15px;
}

#qpfyrmfciw .gt_indent_4 {
  text-indent: 20px;
}

#qpfyrmfciw .gt_indent_5 {
  text-indent: 25px;
}
</style>
<table class="gt_table">
  <thead class="gt_header">
    <tr>
      <td colspan="8" class="gt_heading gt_title gt_font_normal gt_bottom_border" style="font-family: 'Libre Franklin'; font-weight: 800;">Western Conference</td>
    </tr>
    
  </thead>
  <thead class="gt_col_headings">
    <tr>
      <th class="gt_col_heading gt_columns_bottom_border gt_left" rowspan="1" colspan="1" style="color: #A9A9A9; font-family: 'Source Sans Pro'; text-transform: uppercase;" scope="col" id="team_name">team_name</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" style="color: #A9A9A9; font-family: 'Source Sans Pro'; text-transform: uppercase;" scope="col" id="wins">wins</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" style="color: #A9A9A9; font-family: 'Source Sans Pro'; text-transform: uppercase;" scope="col" id="losses">losses</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" style="color: #A9A9A9; font-family: 'Source Sans Pro'; text-transform: uppercase;" scope="col" id="win_loss_pct">win_loss_pct</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_left" rowspan="1" colspan="1" style="color: #A9A9A9; font-family: 'Source Sans Pro'; text-transform: uppercase;" scope="col" id="gb">gb</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" style="color: #A9A9A9; font-family: 'Source Sans Pro'; text-transform: uppercase;" scope="col" id="pts_per_g">pts_per_g</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" style="color: #A9A9A9; font-family: 'Source Sans Pro'; text-transform: uppercase;" scope="col" id="opp_pts_per_g">opp_pts_per_g</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" style="color: #A9A9A9; font-family: 'Source Sans Pro'; text-transform: uppercase;" scope="col" id="srs">srs</th>
    </tr>
  </thead>
  <tbody class="gt_table_body">
    <tr><td headers="team_name" class="gt_row gt_left" style="font-family: 'Source Sans Pro'; font-weight: 400;">Utah Jazz (1) </td>
<td headers="wins" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">12</td>
<td headers="losses" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">7</td>
<td headers="win_loss_pct" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">.632</td>
<td headers="gb" class="gt_row gt_left" style="font-family: 'Source Sans Pro'; font-weight: 400;">—</td>
<td headers="pts_per_g" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">117.4</td>
<td headers="opp_pts_per_g" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">114.5</td>
<td headers="srs" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">2.81</td></tr>
    <tr><td headers="team_name" class="gt_row gt_left" style="font-family: 'Source Sans Pro'; font-weight: 400;">Phoenix Suns (2) </td>
<td headers="wins" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">10</td>
<td headers="losses" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">6</td>
<td headers="win_loss_pct" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">.625</td>
<td headers="gb" class="gt_row gt_left" style="font-family: 'Source Sans Pro'; font-weight: 400;">0.5</td>
<td headers="pts_per_g" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">115.1</td>
<td headers="opp_pts_per_g" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">107.9</td>
<td headers="srs" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">7.19</td></tr>
    <tr><td headers="team_name" class="gt_row gt_left" style="font-family: 'Source Sans Pro'; font-weight: 400;">Denver Nuggets (3) </td>
<td headers="wins" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">10</td>
<td headers="losses" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">6</td>
<td headers="win_loss_pct" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">.625</td>
<td headers="gb" class="gt_row gt_left" style="font-family: 'Source Sans Pro'; font-weight: 400;">0.5</td>
<td headers="pts_per_g" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">113.9</td>
<td headers="opp_pts_per_g" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">113.9</td>
<td headers="srs" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">-0.66</td></tr>
    <tr><td headers="team_name" class="gt_row gt_left" style="font-family: 'Source Sans Pro'; font-weight: 400;">Los Angeles Clippers (4) </td>
<td headers="wins" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">11</td>
<td headers="losses" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">7</td>
<td headers="win_loss_pct" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">.611</td>
<td headers="gb" class="gt_row gt_left" style="font-family: 'Source Sans Pro'; font-weight: 400;">0.5</td>
<td headers="pts_per_g" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">106.1</td>
<td headers="opp_pts_per_g" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">105.8</td>
<td headers="srs" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">-1.02</td></tr>
    <tr><td headers="team_name" class="gt_row gt_left" style="font-family: 'Source Sans Pro'; font-weight: 400;">Sacramento Kings (5) </td>
<td headers="wins" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">9</td>
<td headers="losses" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">6</td>
<td headers="win_loss_pct" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">.600</td>
<td headers="gb" class="gt_row gt_left" style="font-family: 'Source Sans Pro'; font-weight: 400;">1.0</td>
<td headers="pts_per_g" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">121.4</td>
<td headers="opp_pts_per_g" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">117.5</td>
<td headers="srs" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">1.87</td></tr>
    <tr><td headers="team_name" class="gt_row gt_left" style="font-family: 'Source Sans Pro'; font-weight: 400;">New Orleans Pelicans (6) </td>
<td headers="wins" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">10</td>
<td headers="losses" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">7</td>
<td headers="win_loss_pct" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">.588</td>
<td headers="gb" class="gt_row gt_left" style="font-family: 'Source Sans Pro'; font-weight: 400;">1.0</td>
<td headers="pts_per_g" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">116.9</td>
<td headers="opp_pts_per_g" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">110.6</td>
<td headers="srs" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">6.70</td></tr>
    <tr><td headers="team_name" class="gt_row gt_left" style="font-family: 'Source Sans Pro'; font-weight: 400;">Memphis Grizzlies (7) </td>
<td headers="wins" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">10</td>
<td headers="losses" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">7</td>
<td headers="win_loss_pct" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">.588</td>
<td headers="gb" class="gt_row gt_left" style="font-family: 'Source Sans Pro'; font-weight: 400;">1.0</td>
<td headers="pts_per_g" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">114.4</td>
<td headers="opp_pts_per_g" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">114.0</td>
<td headers="srs" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">0.43</td></tr>
    <tr><td headers="team_name" class="gt_row gt_left" style="font-family: 'Source Sans Pro'; font-weight: 400;">Portland Trail Blazers (8) </td>
<td headers="wins" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">10</td>
<td headers="losses" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">7</td>
<td headers="win_loss_pct" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">.588</td>
<td headers="gb" class="gt_row gt_left" style="font-family: 'Source Sans Pro'; font-weight: 400;">1.0</td>
<td headers="pts_per_g" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">109.9</td>
<td headers="opp_pts_per_g" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">108.9</td>
<td headers="srs" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">1.84</td></tr>
    <tr><td headers="team_name" class="gt_row gt_left" style="font-family: 'Source Sans Pro'; font-weight: 400;">Dallas Mavericks (9) </td>
<td headers="wins" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">9</td>
<td headers="losses" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">7</td>
<td headers="win_loss_pct" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">.563</td>
<td headers="gb" class="gt_row gt_left" style="font-family: 'Source Sans Pro'; font-weight: 400;">1.5</td>
<td headers="pts_per_g" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">109.1</td>
<td headers="opp_pts_per_g" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">105.3</td>
<td headers="srs" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">4.08</td></tr>
    <tr><td headers="team_name" class="gt_row gt_left" style="font-family: 'Source Sans Pro'; font-weight: 400;">Minnesota Timberwolves (10) </td>
<td headers="wins" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">9</td>
<td headers="losses" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">8</td>
<td headers="win_loss_pct" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">.529</td>
<td headers="gb" class="gt_row gt_left" style="font-family: 'Source Sans Pro'; font-weight: 400;">2.0</td>
<td headers="pts_per_g" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">114.3</td>
<td headers="opp_pts_per_g" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">114.4</td>
<td headers="srs" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">-1.26</td></tr>
    <tr><td headers="team_name" class="gt_row gt_left" style="font-family: 'Source Sans Pro'; font-weight: 400;">Golden State Warriors (11) </td>
<td headers="wins" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">8</td>
<td headers="losses" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">10</td>
<td headers="win_loss_pct" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">.444</td>
<td headers="gb" class="gt_row gt_left" style="font-family: 'Source Sans Pro'; font-weight: 400;">3.5</td>
<td headers="pts_per_g" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">115.7</td>
<td headers="opp_pts_per_g" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">118.0</td>
<td headers="srs" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">-2.37</td></tr>
    <tr><td headers="team_name" class="gt_row gt_left" style="font-family: 'Source Sans Pro'; font-weight: 400;">Oklahoma City Thunder (12) </td>
<td headers="wins" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">7</td>
<td headers="losses" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">10</td>
<td headers="win_loss_pct" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">.412</td>
<td headers="gb" class="gt_row gt_left" style="font-family: 'Source Sans Pro'; font-weight: 400;">4.0</td>
<td headers="pts_per_g" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">116.4</td>
<td headers="opp_pts_per_g" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">117.5</td>
<td headers="srs" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">-1.41</td></tr>
    <tr><td headers="team_name" class="gt_row gt_left" style="font-family: 'Source Sans Pro'; font-weight: 400;">Los Angeles Lakers (13) </td>
<td headers="wins" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">5</td>
<td headers="losses" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">10</td>
<td headers="win_loss_pct" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">.333</td>
<td headers="gb" class="gt_row gt_left" style="font-family: 'Source Sans Pro'; font-weight: 400;">5.0</td>
<td headers="pts_per_g" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">111.1</td>
<td headers="opp_pts_per_g" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">114.2</td>
<td headers="srs" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">-3.26</td></tr>
    <tr><td headers="team_name" class="gt_row gt_left" style="font-family: 'Source Sans Pro'; font-weight: 400;">San Antonio Spurs (14) </td>
<td headers="wins" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">6</td>
<td headers="losses" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">12</td>
<td headers="win_loss_pct" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">.333</td>
<td headers="gb" class="gt_row gt_left" style="font-family: 'Source Sans Pro'; font-weight: 400;">5.5</td>
<td headers="pts_per_g" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">110.1</td>
<td headers="opp_pts_per_g" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">120.3</td>
<td headers="srs" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">-10.42</td></tr>
    <tr><td headers="team_name" class="gt_row gt_left" style="font-family: 'Source Sans Pro'; font-weight: 400;">Houston Rockets (15) </td>
<td headers="wins" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">3</td>
<td headers="losses" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">14</td>
<td headers="win_loss_pct" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">.176</td>
<td headers="gb" class="gt_row gt_left" style="font-family: 'Source Sans Pro'; font-weight: 400;">8.0</td>
<td headers="pts_per_g" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">108.6</td>
<td headers="opp_pts_per_g" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">116.0</td>
<td headers="srs" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">-6.04</td></tr>
  </tbody>
  
  
</table>
</div>

``` r
eastern_conf_standings %>% gt() %>% gt_theme_nytimes() %>% tab_header(title = "Eastern Conference")
```

<div id="knozqzkaxs" style="padding-left:0px;padding-right:0px;padding-top:10px;padding-bottom:10px;overflow-x:auto;overflow-y:auto;width:auto;height:auto;">
<style>@import url("https://fonts.googleapis.com/css2?family=Source+Sans+Pro:ital,wght@0,100;0,200;0,300;0,400;0,500;0,600;0,700;0,800;0,900;1,100;1,200;1,300;1,400;1,500;1,600;1,700;1,800;1,900&display=swap");
@import url("https://fonts.googleapis.com/css2?family=Libre+Franklin:ital,wght@0,100;0,200;0,300;0,400;0,500;0,600;0,700;0,800;0,900;1,100;1,200;1,300;1,400;1,500;1,600;1,700;1,800;1,900&display=swap");
@import url("https://fonts.googleapis.com/css2?family=Source+Sans+Pro:ital,wght@0,100;0,200;0,300;0,400;0,500;0,600;0,700;0,800;0,900;1,100;1,200;1,300;1,400;1,500;1,600;1,700;1,800;1,900&display=swap");
html {
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Helvetica Neue', 'Fira Sans', 'Droid Sans', Arial, sans-serif;
}

#knozqzkaxs .gt_table {
  display: table;
  border-collapse: collapse;
  margin-left: auto;
  margin-right: auto;
  color: #333333;
  font-size: 16px;
  font-weight: normal;
  font-style: normal;
  background-color: #FFFFFF;
  width: auto;
  border-top-style: none;
  border-top-width: 2px;
  border-top-color: #A8A8A8;
  border-right-style: none;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #A8A8A8;
  border-left-style: none;
  border-left-width: 2px;
  border-left-color: #D3D3D3;
}

#knozqzkaxs .gt_heading {
  background-color: #FFFFFF;
  text-align: left;
  border-bottom-color: #FFFFFF;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
}

#knozqzkaxs .gt_caption {
  padding-top: 4px;
  padding-bottom: 4px;
}

#knozqzkaxs .gt_title {
  color: #333333;
  font-size: 125%;
  font-weight: initial;
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 5px;
  padding-right: 5px;
  border-bottom-color: #FFFFFF;
  border-bottom-width: 0;
}

#knozqzkaxs .gt_subtitle {
  color: #333333;
  font-size: 85%;
  font-weight: initial;
  padding-top: 0;
  padding-bottom: 6px;
  padding-left: 5px;
  padding-right: 5px;
  border-top-color: #FFFFFF;
  border-top-width: 0;
}

#knozqzkaxs .gt_bottom_border {
  border-bottom-style: none;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
}

#knozqzkaxs .gt_col_headings {
  border-top-style: none;
  border-top-width: 2px;
  border-top-color: #D3D3D3;
  border-bottom-style: none;
  border-bottom-width: 1px;
  border-bottom-color: #334422;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
}

#knozqzkaxs .gt_col_heading {
  color: #333333;
  background-color: #FFFFFF;
  font-size: 12px;
  font-weight: normal;
  text-transform: inherit;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
  vertical-align: bottom;
  padding-top: 5px;
  padding-bottom: 6px;
  padding-left: 5px;
  padding-right: 5px;
  overflow-x: hidden;
}

#knozqzkaxs .gt_column_spanner_outer {
  color: #333333;
  background-color: #FFFFFF;
  font-size: 12px;
  font-weight: normal;
  text-transform: inherit;
  padding-top: 0;
  padding-bottom: 0;
  padding-left: 4px;
  padding-right: 4px;
}

#knozqzkaxs .gt_column_spanner_outer:first-child {
  padding-left: 0;
}

#knozqzkaxs .gt_column_spanner_outer:last-child {
  padding-right: 0;
}

#knozqzkaxs .gt_column_spanner {
  border-bottom-style: none;
  border-bottom-width: 1px;
  border-bottom-color: #334422;
  vertical-align: bottom;
  padding-top: 5px;
  padding-bottom: 5px;
  overflow-x: hidden;
  display: inline-block;
  width: 100%;
}

#knozqzkaxs .gt_group_heading {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: initial;
  text-transform: inherit;
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
  vertical-align: middle;
  text-align: left;
}

#knozqzkaxs .gt_empty_group_heading {
  padding: 0.5px;
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: initial;
  border-top-style: solid;
  border-top-width: 2px;
  border-top-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  vertical-align: middle;
}

#knozqzkaxs .gt_from_md > :first-child {
  margin-top: 0;
}

#knozqzkaxs .gt_from_md > :last-child {
  margin-bottom: 0;
}

#knozqzkaxs .gt_row {
  padding-top: 7px;
  padding-bottom: 7px;
  padding-left: 5px;
  padding-right: 5px;
  margin: 10px;
  border-top-style: solid;
  border-top-width: 1px;
  border-top-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 1px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 1px;
  border-right-color: #D3D3D3;
  vertical-align: middle;
  overflow-x: hidden;
}

#knozqzkaxs .gt_stub {
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: initial;
  text-transform: inherit;
  border-right-style: solid;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
  padding-left: 5px;
  padding-right: 5px;
}

#knozqzkaxs .gt_stub_row_group {
  color: #333333;
  background-color: #FFFFFF;
  font-size: 100%;
  font-weight: initial;
  text-transform: inherit;
  border-right-style: solid;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
  padding-left: 5px;
  padding-right: 5px;
  vertical-align: top;
}

#knozqzkaxs .gt_row_group_first td {
  border-top-width: 2px;
}

#knozqzkaxs .gt_summary_row {
  color: #333333;
  background-color: #FFFFFF;
  text-transform: inherit;
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
}

#knozqzkaxs .gt_first_summary_row {
  border-top-style: solid;
  border-top-color: #D3D3D3;
}

#knozqzkaxs .gt_first_summary_row.thick {
  border-top-width: 2px;
}

#knozqzkaxs .gt_last_summary_row {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
}

#knozqzkaxs .gt_grand_summary_row {
  color: #333333;
  background-color: #FFFFFF;
  text-transform: inherit;
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
}

#knozqzkaxs .gt_first_grand_summary_row {
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 5px;
  padding-right: 5px;
  border-top-style: double;
  border-top-width: 6px;
  border-top-color: #D3D3D3;
}

#knozqzkaxs .gt_striped {
  background-color: rgba(128, 128, 128, 0.05);
}

#knozqzkaxs .gt_table_body {
  border-top-style: none;
  border-top-width: 2px;
  border-top-color: #D3D3D3;
  border-bottom-style: solid;
  border-bottom-width: 2px;
  border-bottom-color: #FFFFFF;
}

#knozqzkaxs .gt_footnotes {
  color: #333333;
  background-color: #FFFFFF;
  border-bottom-style: none;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 2px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
}

#knozqzkaxs .gt_footnote {
  margin: 0px;
  font-size: 90%;
  padding-left: 4px;
  padding-right: 4px;
  padding-left: 5px;
  padding-right: 5px;
}

#knozqzkaxs .gt_sourcenotes {
  color: #333333;
  background-color: #FFFFFF;
  border-bottom-style: none;
  border-bottom-width: 2px;
  border-bottom-color: #D3D3D3;
  border-left-style: none;
  border-left-width: 2px;
  border-left-color: #D3D3D3;
  border-right-style: none;
  border-right-width: 2px;
  border-right-color: #D3D3D3;
}

#knozqzkaxs .gt_sourcenote {
  font-size: 90%;
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 5px;
  padding-right: 5px;
}

#knozqzkaxs .gt_left {
  text-align: left;
}

#knozqzkaxs .gt_center {
  text-align: center;
}

#knozqzkaxs .gt_right {
  text-align: right;
  font-variant-numeric: tabular-nums;
}

#knozqzkaxs .gt_font_normal {
  font-weight: normal;
}

#knozqzkaxs .gt_font_bold {
  font-weight: bold;
}

#knozqzkaxs .gt_font_italic {
  font-style: italic;
}

#knozqzkaxs .gt_super {
  font-size: 65%;
}

#knozqzkaxs .gt_footnote_marks {
  font-style: italic;
  font-weight: normal;
  font-size: 75%;
  vertical-align: 0.4em;
}

#knozqzkaxs .gt_asterisk {
  font-size: 100%;
  vertical-align: 0;
}

#knozqzkaxs .gt_indent_1 {
  text-indent: 5px;
}

#knozqzkaxs .gt_indent_2 {
  text-indent: 10px;
}

#knozqzkaxs .gt_indent_3 {
  text-indent: 15px;
}

#knozqzkaxs .gt_indent_4 {
  text-indent: 20px;
}

#knozqzkaxs .gt_indent_5 {
  text-indent: 25px;
}
</style>
<table class="gt_table">
  <thead class="gt_header">
    <tr>
      <td colspan="8" class="gt_heading gt_title gt_font_normal gt_bottom_border" style="font-family: 'Libre Franklin'; font-weight: 800;">Eastern Conference</td>
    </tr>
    
  </thead>
  <thead class="gt_col_headings">
    <tr>
      <th class="gt_col_heading gt_columns_bottom_border gt_left" rowspan="1" colspan="1" style="color: #A9A9A9; font-family: 'Source Sans Pro'; text-transform: uppercase;" scope="col" id="team_name">team_name</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" style="color: #A9A9A9; font-family: 'Source Sans Pro'; text-transform: uppercase;" scope="col" id="wins">wins</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" style="color: #A9A9A9; font-family: 'Source Sans Pro'; text-transform: uppercase;" scope="col" id="losses">losses</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" style="color: #A9A9A9; font-family: 'Source Sans Pro'; text-transform: uppercase;" scope="col" id="win_loss_pct">win_loss_pct</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_left" rowspan="1" colspan="1" style="color: #A9A9A9; font-family: 'Source Sans Pro'; text-transform: uppercase;" scope="col" id="gb">gb</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" style="color: #A9A9A9; font-family: 'Source Sans Pro'; text-transform: uppercase;" scope="col" id="pts_per_g">pts_per_g</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" style="color: #A9A9A9; font-family: 'Source Sans Pro'; text-transform: uppercase;" scope="col" id="opp_pts_per_g">opp_pts_per_g</th>
      <th class="gt_col_heading gt_columns_bottom_border gt_right" rowspan="1" colspan="1" style="color: #A9A9A9; font-family: 'Source Sans Pro'; text-transform: uppercase;" scope="col" id="srs">srs</th>
    </tr>
  </thead>
  <tbody class="gt_table_body">
    <tr><td headers="team_name" class="gt_row gt_left" style="font-family: 'Source Sans Pro'; font-weight: 400;">Boston Celtics (1) </td>
<td headers="wins" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">13</td>
<td headers="losses" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">4</td>
<td headers="win_loss_pct" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">.765</td>
<td headers="gb" class="gt_row gt_left" style="font-family: 'Source Sans Pro'; font-weight: 400;">—</td>
<td headers="pts_per_g" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">119.4</td>
<td headers="opp_pts_per_g" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">113.5</td>
<td headers="srs" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">6.10</td></tr>
    <tr><td headers="team_name" class="gt_row gt_left" style="font-family: 'Source Sans Pro'; font-weight: 400;">Milwaukee Bucks (2) </td>
<td headers="wins" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">12</td>
<td headers="losses" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">4</td>
<td headers="win_loss_pct" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">.750</td>
<td headers="gb" class="gt_row gt_left" style="font-family: 'Source Sans Pro'; font-weight: 400;">0.5</td>
<td headers="pts_per_g" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">111.4</td>
<td headers="opp_pts_per_g" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">106.9</td>
<td headers="srs" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">3.17</td></tr>
    <tr><td headers="team_name" class="gt_row gt_left" style="font-family: 'Source Sans Pro'; font-weight: 400;">Cleveland Cavaliers (3) </td>
<td headers="wins" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">11</td>
<td headers="losses" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">6</td>
<td headers="win_loss_pct" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">.647</td>
<td headers="gb" class="gt_row gt_left" style="font-family: 'Source Sans Pro'; font-weight: 400;">2.0</td>
<td headers="pts_per_g" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">115.6</td>
<td headers="opp_pts_per_g" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">108.2</td>
<td headers="srs" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">6.89</td></tr>
    <tr><td headers="team_name" class="gt_row gt_left" style="font-family: 'Source Sans Pro'; font-weight: 400;">Indiana Pacers (4) </td>
<td headers="wins" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">10</td>
<td headers="losses" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">6</td>
<td headers="win_loss_pct" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">.625</td>
<td headers="gb" class="gt_row gt_left" style="font-family: 'Source Sans Pro'; font-weight: 400;">2.5</td>
<td headers="pts_per_g" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">116.8</td>
<td headers="opp_pts_per_g" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">114.1</td>
<td headers="srs" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">1.19</td></tr>
    <tr><td headers="team_name" class="gt_row gt_left" style="font-family: 'Source Sans Pro'; font-weight: 400;">Washington Wizards (5) </td>
<td headers="wins" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">10</td>
<td headers="losses" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">7</td>
<td headers="win_loss_pct" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">.588</td>
<td headers="gb" class="gt_row gt_left" style="font-family: 'Source Sans Pro'; font-weight: 400;">3.0</td>
<td headers="pts_per_g" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">108.6</td>
<td headers="opp_pts_per_g" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">109.4</td>
<td headers="srs" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">-0.26</td></tr>
    <tr><td headers="team_name" class="gt_row gt_left" style="font-family: 'Source Sans Pro'; font-weight: 400;">Atlanta Hawks (6) </td>
<td headers="wins" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">10</td>
<td headers="losses" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">7</td>
<td headers="win_loss_pct" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">.588</td>
<td headers="gb" class="gt_row gt_left" style="font-family: 'Source Sans Pro'; font-weight: 400;">3.0</td>
<td headers="pts_per_g" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">114.4</td>
<td headers="opp_pts_per_g" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">114.4</td>
<td headers="srs" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">0.45</td></tr>
    <tr><td headers="team_name" class="gt_row gt_left" style="font-family: 'Source Sans Pro'; font-weight: 400;">Toronto Raptors (7) </td>
<td headers="wins" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">9</td>
<td headers="losses" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">8</td>
<td headers="win_loss_pct" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">.529</td>
<td headers="gb" class="gt_row gt_left" style="font-family: 'Source Sans Pro'; font-weight: 400;">4.0</td>
<td headers="pts_per_g" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">112.5</td>
<td headers="opp_pts_per_g" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">110.0</td>
<td headers="srs" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">2.24</td></tr>
    <tr><td headers="team_name" class="gt_row gt_left" style="font-family: 'Source Sans Pro'; font-weight: 400;">New York Knicks (8) </td>
<td headers="wins" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">9</td>
<td headers="losses" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">9</td>
<td headers="win_loss_pct" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">.500</td>
<td headers="gb" class="gt_row gt_left" style="font-family: 'Source Sans Pro'; font-weight: 400;">4.5</td>
<td headers="pts_per_g" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">113.3</td>
<td headers="opp_pts_per_g" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">115.5</td>
<td headers="srs" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">-2.31</td></tr>
    <tr><td headers="team_name" class="gt_row gt_left" style="font-family: 'Source Sans Pro'; font-weight: 400;">Philadelphia 76ers (9) </td>
<td headers="wins" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">8</td>
<td headers="losses" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">8</td>
<td headers="win_loss_pct" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">.500</td>
<td headers="gb" class="gt_row gt_left" style="font-family: 'Source Sans Pro'; font-weight: 400;">4.5</td>
<td headers="pts_per_g" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">108.6</td>
<td headers="opp_pts_per_g" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">106.6</td>
<td headers="srs" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">3.05</td></tr>
    <tr><td headers="team_name" class="gt_row gt_left" style="font-family: 'Source Sans Pro'; font-weight: 400;">Brooklyn Nets (10) </td>
<td headers="wins" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">8</td>
<td headers="losses" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">9</td>
<td headers="win_loss_pct" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">.471</td>
<td headers="gb" class="gt_row gt_left" style="font-family: 'Source Sans Pro'; font-weight: 400;">5.0</td>
<td headers="pts_per_g" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">111.6</td>
<td headers="opp_pts_per_g" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">111.6</td>
<td headers="srs" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">0.99</td></tr>
    <tr><td headers="team_name" class="gt_row gt_left" style="font-family: 'Source Sans Pro'; font-weight: 400;">Chicago Bulls (11) </td>
<td headers="wins" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">7</td>
<td headers="losses" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">10</td>
<td headers="win_loss_pct" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">.412</td>
<td headers="gb" class="gt_row gt_left" style="font-family: 'Source Sans Pro'; font-weight: 400;">6.0</td>
<td headers="pts_per_g" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">111.1</td>
<td headers="opp_pts_per_g" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">111.3</td>
<td headers="srs" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">1.39</td></tr>
    <tr><td headers="team_name" class="gt_row gt_left" style="font-family: 'Source Sans Pro'; font-weight: 400;">Miami Heat (12) </td>
<td headers="wins" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">7</td>
<td headers="losses" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">11</td>
<td headers="win_loss_pct" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">.389</td>
<td headers="gb" class="gt_row gt_left" style="font-family: 'Source Sans Pro'; font-weight: 400;">6.5</td>
<td headers="pts_per_g" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">108.2</td>
<td headers="opp_pts_per_g" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">109.8</td>
<td headers="srs" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">-0.57</td></tr>
    <tr><td headers="team_name" class="gt_row gt_left" style="font-family: 'Source Sans Pro'; font-weight: 400;">Orlando Magic (13) </td>
<td headers="wins" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">5</td>
<td headers="losses" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">13</td>
<td headers="win_loss_pct" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">.278</td>
<td headers="gb" class="gt_row gt_left" style="font-family: 'Source Sans Pro'; font-weight: 400;">8.5</td>
<td headers="pts_per_g" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">109.5</td>
<td headers="opp_pts_per_g" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">113.5</td>
<td headers="srs" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">-3.95</td></tr>
    <tr><td headers="team_name" class="gt_row gt_left" style="font-family: 'Source Sans Pro'; font-weight: 400;">Charlotte Hornets (14) </td>
<td headers="wins" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">4</td>
<td headers="losses" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">14</td>
<td headers="win_loss_pct" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">.222</td>
<td headers="gb" class="gt_row gt_left" style="font-family: 'Source Sans Pro'; font-weight: 400;">9.5</td>
<td headers="pts_per_g" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">109.5</td>
<td headers="opp_pts_per_g" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">115.2</td>
<td headers="srs" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">-5.88</td></tr>
    <tr><td headers="team_name" class="gt_row gt_left" style="font-family: 'Source Sans Pro'; font-weight: 400;">Detroit Pistons (15) </td>
<td headers="wins" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">3</td>
<td headers="losses" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">15</td>
<td headers="win_loss_pct" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">.167</td>
<td headers="gb" class="gt_row gt_left" style="font-family: 'Source Sans Pro'; font-weight: 400;">10.5</td>
<td headers="pts_per_g" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">109.4</td>
<td headers="opp_pts_per_g" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">118.6</td>
<td headers="srs" class="gt_row gt_right" style="font-family: 'Source Sans Pro'; font-weight: 400;">-8.35</td></tr>
  </tbody>
  
  
</table>
</div>

Making a graph using the standings table

``` r
western_conf_standings$conf <- "West"
eastern_conf_standings$conf <- "East"
western_conf_standings$West_win_loss_pct <- as.numeric(western_conf_standings$win_loss_pct)
eastern_conf_standings$East_win_loss_pct <- as.numeric(eastern_conf_standings$win_loss_pct)
western_conf_standings$opp_pts_per_g <- as.numeric(western_conf_standings$opp_pts_per_g)
eastern_conf_standings$opp_pts_per_g <- as.numeric(eastern_conf_standings$opp_pts_per_g)
western_conf_standings$pts_per_g <- as.numeric(western_conf_standings$pts_per_g)
eastern_conf_standings$pts_per_g <- as.numeric(eastern_conf_standings$pts_per_g)
ggplot() +
  geom_text(data = western_conf_standings, aes(x = pts_per_g, y = opp_pts_per_g, label = regmatches(team_name, gregexpr("(?=\\().*?(?<=\\))", team_name, perl=T)), color = West_win_loss_pct))+
  ggtitle("League Standings (Team Rank)")+
  scale_color_gradient2("West_win_loss_pct",low = "#FA8072", high = "#D30000")+
  new_scale("color")+
  geom_text(data = eastern_conf_standings, aes(x = pts_per_g, y = opp_pts_per_g, label = regmatches(team_name, gregexpr("(?=\\().*?(?<=\\))", team_name, perl=T)), color = East_win_loss_pct))+
  scale_color_gradient2("East_win_loss_pct",low = "#29C5F6", high = "#1260CC")+
  theme(
    axis.text.x = element_text(size = 12),
    axis.text.y = element_text(size = 12)
  )
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-4-1.png" width="672" />
