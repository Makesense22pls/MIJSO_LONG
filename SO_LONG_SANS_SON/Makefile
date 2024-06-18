# **************************************************************************** #
#                                                                              #
#                                                         :::      ::::::::    #
#    Makefile                                           :+:      :+:    :+:    #
#                                                     +:+ +:+         +:+      #
#    By: mafourni <mafourni@student.42.fr>          +#+  +:+       +#+         #
#                                                 +#+#+#+#+#+   +#+            #
#    Created: 2024/04/05 17:01:19 by mafourni          #+#    #+#              #
#    Updated: 2024/06/18 16:54:25 by mafourni         ###   ########.fr        #
#                                                                              #
# **************************************************************************** #

NAME = so_long
# CFLAGS = -Wall -Werror -Wextra -g -fsanitize=address
CFLAGS = -Wall -Werror -Wextra -g 
RM = rm -f
CC = gcc

SRC = exec/image_player.c exec/text_and_resume.c utils/free.c utils/innit.c parsing/flood_fill.c exec/sound_and_change_image.c exec/direction_key.c exec/key_press.c parsing/check_arg.c parsing/check_fd/full_map.c exec/main.c parsing/check_fd/check_place.c exec/image.c

OBJ = $(SRC:.c=.o)

LIBFT_DIR = libft
LIBFT_LIB = $(LIBFT_DIR)/libft.a

MLX42_REPO = https://github.com/codam-coding-college/MLX42.git
MLX42_DIR = MLX42
MLX42_BUILD_DIR = $(MLX42_DIR)/build
MLX42_LIB = $(MLX42_BUILD_DIR)/libmlx42.a

USER = $(shell whoami)

HEADERS_MLX42 = $(MLX42_DIR)/include/MLX42
HEADERS_GLFW = /Users/$(USER)/homebrew/opt/glfw/lib
HEADERS_LIB = $(LIBFT_DIR)

all: $(LIBFT_LIB) mlx42 $(NAME)

$(LIBFT_LIB):
	@make -C $(LIBFT_DIR)

mlx42 :
		@git clone $(MLX42_REPO) $(MLX42_DIR)
		@cd $(MLX42_DIR) && cmake -B build
		@cd $(MLX42_DIR) && cmake --build build -j4

%.o: %.c
	$(CC) $(CFLAGS) -I. -I$(HEADERS_MLX42) -I$(HEADERS_GLFW) -I$(HEADERS_LIB) -c $< -o $@ 

$(NAME): $(OBJ)
	$(CC) $(CFLAGS) $(OBJ) -I. -I$(HEADERS_MLX42) -L$(HEADERS_GLFW) -I$(HEADERS_LIB) -L$(LIBFT_DIR) -lft -L$(MLX42_BUILD_DIR) -lmlx42 -ldl -lglfw -pthread -lm  -framework Cocoa -framework OpenGL -framework IOKit -o $@

clean:
	$(RM) $(OBJ)
	@make clean -C $(LIBFT_DIR)
	@make clean -C $(MLX42_BUILD_DIR)

fclean: clean
	$(RM) $(NAME)
	@make fclean -C $(LIBFT_DIR)
	$(RM) -r $(MLX42_DIR)

re: fclean all

