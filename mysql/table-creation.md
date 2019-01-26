```
ALTER TABLE `imoocsvr`.`product_resource` 
ADD COLUMN `deadline` INT NOT NULL DEFAULT 3 AFTER `state`,
ADD COLUMN `score` INT NOT NULL DEFAULT 2 AFTER `deadline`,
ADD COLUMN `is_required` INT NOT NULL DEFAULT 0 AFTER `score`;

ALTER TABLE `imoocsvr`.`exam` 
CHANGE COLUMN `image` `image` VARCHAR(128) NOT NULL ;

ALTER TABLE `imoocsvr`.`product_user` 
ADD COLUMN `study_progress` INT(11) NOT NULL DEFAULT 0 AFTER `is_evaluate`;

CREATE TABLE `imoocsvr`.`schedule_process_data` (
  `id` VARCHAR(45) NOT NULL,
  `team_id` VARCHAR(45) NOT NULL,
  `user_id` VARCHAR(45) NOT NULL,
  `course_id` VARCHAR(45) NOT NULL,
  `target_id` VARCHAR(45) NOT NULL,
  `target_type` INT(2) NOT NULL DEFAULT 1,
  `play_time` INT(30) NOT NULL DEFAULT 0,
  `playing_point` INT(11) NOT NULL DEFAULT 0,
  `data_amount` INT(30) NOT NULL DEFAULT 0,
  `schedule` INT(11) NOT NULL DEFAULT 0,
  `play_count` INT(11) NOT NULL DEFAULT 0,
  `add_time_int` INT(11) NOT NULL,
  `add_time_str` VARCHAR(45) NOT NULL,
  PRIMARY KEY (`id`))
ENGINE = MyISAM
DEFAULT CHARACTER SET = utf8;

CREATE UNIQUE INDEX schedule_process_data_team_id_user_id_course_id_target_id_uindex ON schedule_process_data (team_id, user_id, course_id, target_id);
CREATE INDEX schedule_process_data_course_id_index ON schedule_process_data (course_id);
CREATE INDEX schedule_process_data_play_count_index ON schedule_process_data (play_count DESC);
CREATE INDEX schedule_process_data_play_time_index ON schedule_process_data (play_time DESC);
CREATE INDEX schedule_process_data_data_amount_index ON schedule_process_data (data_amount DESC);
CREATE INDEX schedule_process_data_add_time_int_index ON schedule_process_data (add_time_int DESC);

DROP INDEX schedule_process_data_data_amount_index ON schedule_process_data;
DROP INDEX schedule_process_data_play_count_index ON schedule_process_data;
DROP INDEX schedule_process_data_play_time_index ON schedule_process_data;
DROP INDEX schedule_process_data_team_id_user_id_course_id_target_id_uindex ON schedule_process_data;

